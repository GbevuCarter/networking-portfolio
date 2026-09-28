# Lab: 2-Router Static Routing

**Date:** 2026-09-26
**Tool:** Cisco Packet Tracer

## Objective
Configure two routers with static routes so that devices on separate networks can communicate with each other.

## Topology

PC0 -- Router0 -- Router1 -- PC1

| Device   | Interface | IP Address        |
|----------|-----------|--------------------|
| PC0      | —         | 192.168.1.10 /24 (gateway 192.168.1.1) |
| Router0  | Gi0/0/0   | 192.168.1.1 /24   |
| Router0  | Gi0/0/1   | 10.0.0.1 /30       |
| Router1  | Gi0/0/0   | 10.0.0.2 /30       |
| Router1  | Gi0/0/1   | 192.168.3.1 /24   |
| PC1      | —         | 192.168.3.20 /24 (gateway 192.168.3.1) |

The link between Router0 and Router1 uses a /30 subnet — just enough for the two point-to-point addresses.

## Configuration

**Router0** — specific static route to reach PC1's network:
ip route 192.168.3.0 255.255.255.0 10.0.0.2


**Router1** — default route back toward Router0:
ip route 0.0.0.0 0.0.0.0 10.0.0.1


## Verification
Confirmed connectivity end-to-end with `ping` between PC0 and PC1, and verified both routes with `show running-config` on each router.

## What I learned
- A specific static route names an exact destination network; a default route (`0.0.0.0 0.0.0.0`) matches *any* destination not otherwise known.
- A default route makes sense when a router has only one way out of its network — since Router1 only had one exit path, a default route worked just as well as listing the destination explicitly.
- Either router in this topology could have used a default route, since both only had a single link out. The choice isn't forced by topology alone — it's a design decision.
