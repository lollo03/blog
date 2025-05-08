+++
title = 'Tunneling Web Traffic to a Kubernetes Cluster Using WireGuard and a VPS'
date = 2025-05-08T11:30:58+02:00
draft = false
+++

Tunneling traffic securely from the internet to a private Kubernetes cluster can be tricky—especially if your cluster runs in a restricted or local network environment. In this guide, I’ll show you how I used **WireGuard** and a **VPS** to expose services running in a Kubernetes cluster to the public internet.

## Requirement

You will need:
- Your working Kubernetes cluster
- A VPS with a public IP address (a good free VPS is [oracle free tier](https://www.oracle.com/cloud/free/))

## Step 1: Wireguard setup

We'll use **WireGuard** WireGuard to tunnel traffic from the VPS (which is internet-accessible) to the private Kubernetes node. to tunnel traffic from the VPS (which is internet-accessible) to the private Kubernetes node.

First, **install WireGuard** on both your VPS and the Kubernetes server.

> If you are comfortable with ansible, you can also use [this](https://github.com/lollo03/wireguard-forward-ansible) playbook.

On the VPS, create a WireGuard configuration file like this:
```conf
[Interface]
Address = 10.69.0.1/16
ListenPort = 51820
PrivateKey = <Vps privateKey>

# packet forwarding
PreUp = sysctl -w net.ipv4.ip_forward=1

# MASQUERADE
PreUp = iptables -t nat -A POSTROUTING -o wg0 -j MASQUERADE
PostDown = iptables -t nat -D POSTROUTING -o wg0 -j MASQUERADE

# port forwarding
PreUp = iptables -t nat -A PREROUTING -i ens3 -p tcp --dport 80 -j DNAT --to-destination 10.69.1.1:80
PreUp = iptables -t nat -A PREROUTING -i ens3 -p tcp --dport 443 -j DNAT --to-destination 10.69.1.1:443
PostDown = iptables -t nat -D PREROUTING -i ens3 -p tcp --dport 443 -j DNAT --to-destination 10.69.1.1:443
PostDown = iptables -t nat -D PREROUTING -i ens3 -p tcp --dport 80 -j DNAT --to-destination 10.69.1.1:80

[Peer]
PublicKey = <Kubernetes server publicKey>
AllowedIPs = 10.69.1.1, 10.69.0.2
```
**Double-check** your configuration and adjust the iptables rules to match your environment—specifically, update the interface name if it differs.

On the Kubernetes server, use the following configuration:
```conf
[Interface]
PrivateKey = <Kubernetes server privateKey>
Address = 10.69.0.2/16

[Peer]
PublicKey = <Vps publicKey>
Endpoint = <VPS IP>:51820
AllowedIPs = 10.69.0.1
PersistentKeepalive = 25
```

Finally, **check your firewall rules** and ensure that incoming traffic is allowed on ports 80 and 443.

## Step 2: Kubernetes setup

Install MetalLB and create an IP address pool using Helm (or kubectl).

I like to use helmfiles and [mettallb-config](https://gitlab.poul.org/sysadmin/kubernetes/charts/metallb-config) for advanced configuration like this one.

```yaml
#mettallb-config values
extraDeploy:
  - |
    apiVersion: metallb.io/v1beta1
    kind: IPAddressPool
    metadata:
      name: ippool-wireguard
      namespace: metallb
    spec:
      addresses:
        - 10.69.1.0/24
      autoAssign: true
      avoidBuggyIPs: true
  - |
    apiVersion: metallb.io/v1beta1
    kind: L2Advertisement
    metadata:
      name: default
      namespace: metallb
    spec:
      ipAddressPools:
        - ippool-wireguard
```

This sets up a static IP range (`10.69.1.0/24`) for MetalLB to assign to services.

Install an **ingress** controller such as [ingress-nginx](https://github.com/kubernetes/ingress-nginx) and configure it to use a **static IP** from MetalLB:

```yaml
#ingress-nginx values
controller:
    ...
    service:
    ...
    annotations:
        metallb.universe.tf/loadBalancerIPs: 10.69.1.1  
```

This binds your ingress controller’s service to the IP `10.69.1.1`, which the VPS is already routing traffic to via WireGuard.

