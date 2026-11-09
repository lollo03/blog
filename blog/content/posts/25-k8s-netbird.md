+++
title = 'Expose Services from Your Kubernetes Cluster Safely with NetBird'
date = 2026-11-09T18:31:20+01:00
draft = false
+++

Do you want to expose services running in your Kubernetes cluster without opening a single port on your router? In this step-by-step guide I'll show you how I did it with [NetBird](https://netbird.io/), using plain Kubernetes resources and **no operator**.

The idea is simple: NetBird runs on the cluster nodes and acts as a routing peer, so devices connected to your NetBird network can reach the cluster's ingress IP directly. Only authenticated peers can access it, and nothing is exposed to the public internet.

## Prerequisites

- A working Kubernetes cluster
- [MetalLB](https://metallb.universe.tf/) installed (or another way to give a Service a fixed IP)
- A NetBird account

## Initial setup

First, go to [netbird.io](https://netbird.io/) and create a free account. The free plan gives you 100 peers and 5 users, which is plenty for a homelab.

Then install NetBird on every Kubernetes node following the [official guide](https://docs.netbird.io/get-started/install/linux) and run:

```bash
netbird up
```

This registers the node as a peer and starts the NetBird service. Repeat the same steps on all the nodes that will act as routing peers.

## Give the ingress a fixed IP with MetalLB

Now we need an IP address that the cluster listens on and that NetBird can route to. I'll use **MetalLB** as the load balancer and reserve a single address for it:

```yaml
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: netbird-pool
  namespace: metallb-system
spec:
  addresses:
    - 10.35.0.200/32
  autoAssign: false
  avoidBuggyIPs: false
```

A few notes:

- The `/32` is intentional: we only need one IP.
- `autoAssign: false` means MetalLB won't hand this IP to random Services; we'll assign it explicitly.
- Do **not** add this pool to an `L2Advertisement`. We don't need MetalLB to advertise the IP over ARP on the LAN: traffic arrives from the NetBird routing peer and is handled locally by kube-proxy, so there is nothing to announce.

Then point your ingress controller/gateway at that address.

## NetBird setup

Head to the [NetBird console](https://app.netbird.io/) and go to **Network Routing → Networks → Add Network**.

1. Give the network a name, for example `k8s`.
2. Add a **resource** with the IP the cluster listens on, in my example `10.35.0.200/32`.
3. Add a **policy** to control who can access it. The cleanest way is to create a **group** (for example `homelab-admins`) and allow traffic from that group to the resource.
4. Add **routing peers**: select all your Kubernetes nodes.

That's it. Any device in the allowed group can now reach `10.35.0.200` as if it were on the same network, while everyone else can't even see it.

## DNS setup

Typing IP addresses is not fun, so you probably want DNS records like `service.netbird.example.com`.

My solution is to use [external-dns](https://github.com/kubernetes-sigs/external-dns) to create the records automatically. However, that alone is not enough: most home routers and mobile carriers refuse to resolve public DNS names to private IPs (like our `10.35.0.200`).

To fix this, add a wildcard record in NetBird's own DNS zone:

1. Open the NetBird console and go to **DNS → Zones**.
2. Add a record for `*.netbird.example.com` pointing to `10.35.0.200`.

Devices connected to NetBird will use this zone and resolve the name correctly, while public DNS can keep pointing wherever you want (or nowhere at all).

## Wrapping up

With a NetBird network, a MetalLB pool and a wildcard DNS zone you get a private, authenticated entry point to every service in your cluster — no port forwarding, no public IPs and no extra operator to maintain.

Happy self-hosting!
