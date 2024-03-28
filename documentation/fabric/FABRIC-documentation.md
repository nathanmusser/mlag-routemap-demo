# FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| FABRIC | l3leaf | agg1 | 192.168.0.111/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | agg2 | 192.168.0.112/24 | vEOS-lab | Provisioned | - |
| FABRIC | l2leaf | leaf1 | 192.168.0.121/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | spine1 | 192.168.0.101/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | spine2 | 192.168.0.102/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | agg1 | Ethernet1 | spine | spine1 | Ethernet1 |
| l3leaf | agg1 | Ethernet2 | spine | spine2 | Ethernet1 |
| l3leaf | agg1 | Ethernet3 | mlag_peer | agg2 | Ethernet3 |
| l3leaf | agg1 | Ethernet4 | mlag_peer | agg2 | Ethernet4 |
| l3leaf | agg1 | Ethernet5 | l2leaf | leaf1 | Ethernet1 |
| l3leaf | agg2 | Ethernet1 | spine | spine1 | Ethernet2 |
| l3leaf | agg2 | Ethernet2 | spine | spine2 | Ethernet2 |
| l3leaf | agg2 | Ethernet5 | l2leaf | leaf1 | Ethernet2 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 192.168.202.0/24 | 256 | 8 | 3.13 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| agg1 | Ethernet1 | 192.168.202.1/31 | spine1 | Ethernet1 | 192.168.202.0/31 |
| agg1 | Ethernet2 | 192.168.202.3/31 | spine2 | Ethernet1 | 192.168.202.2/31 |
| agg2 | Ethernet1 | 192.168.202.5/31 | spine1 | Ethernet2 | 192.168.202.4/31 |
| agg2 | Ethernet2 | 192.168.202.7/31 | spine2 | Ethernet2 | 192.168.202.6/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.200.0/24 | 256 | 4 | 1.57 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | agg1 | 192.168.200.3/32 |
| FABRIC | agg2 | 192.168.200.4/32 |
| FABRIC | spine1 | 192.168.200.1/32 |
| FABRIC | spine2 | 192.168.200.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.201.0/24 | 256 | 2 | 0.79 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | agg1 | 192.168.201.3/32 |
| FABRIC | agg2 | 192.168.201.3/32 |
