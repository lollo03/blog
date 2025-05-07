+++
title = 'Tunneling Web Traffic to a Kubernetes Cluster Using WireGuard and a VPS'
date = 2025-05-07T12:07:58+02:00
draft = true
+++

Hi everyone, today I’ll show you how I built a setup capable of hosting services on the web by accepting traffic from a VPS that tunnels traffic via WireGuard to another server running Kubernetes.

## Requirement

You will need:
- Your working Kubernetes cluster
- A VPS (a good free VPS is [oracle free tier](https://www.oracle.com/cloud/free/))

## Wireguard setup

We will use WireGuard to tunnel **traffic from the internet** to our Kubernetes cluster.

First, **install WireGuard** on both your VPS and the Kubernetes server.

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

## Kubernetes setup

Install metallb, and create an IP pool (TODO)

Create a new ingress, i like to use [ingress-nginx](https://github.com/kubernetes/ingress-nginx). Add an annotation to your (TODO)
