<div align="center">

# 🌐 Enterprise Routing & High Availability Labs

[![Domain](https://img.shields.io/badge/Domain-Enterprise_Routing_&_WAN-00599C?style=for-the-badge&logo=cisco&logoColor=white)](https://cisco.com)
[![Platform](https://img.shields.io/badge/Platform-Cisco_IOS_15.1_/_12.4-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)](https://cisco.com)
[![Protocols](https://img.shields.io/badge/Protocols-OSPF_|_EIGRP_|_HSRP_|_Static_|_ECMP-brightgreen?style=for-the-badge)]()
[![Hardware](https://img.shields.io/badge/Devices-Cisco_2911_|_2811_|_1841-orange?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Portfolio_Status-5_Labs_Verified-success?style=for-the-badge)]()

<p align="center">
  <b>A comprehensive hands-on engineering portfolio covering Dynamic Routing Protocols (OSPF Multi-Area & EIGRP), High-Availability Gateway Redundancy (HSRP), Multi-Hop Static Routing, and Full-Mesh WAN ECMP Load Balancing.</b>
</p>

</div>

---

## 📌 Executive Overview

This repository demonstrates the architecture, configuration, and verification of enterprise-grade Layer 3 routing topologies. Each lab represents a distinct enterprise routing scenario built and validated using Cisco IOS routers (Cisco 2911, 2811, and 1841 series).

All configurations emphasize **deterministic path selection**, **sub-second convergence**, **redundancy without single points of failure**, and **systematic CLI verification**.

---

## 🗺️ Master Lab Catalog & Navigation

| Lab Directory | Topic & Architecture | Key Protocols & Technologies | Target Devices | Verification Highlights |
| :--- | :--- | :--- | :--- | :--- |
| [**`01-dynamic-routing-eigrp`**](./01-dynamic-routing-eigrp) | Branch-to-Hub Interconnect | EIGRP AS 7, DUAL Algorithm, Composite Metric | 2x Cisco 2811 | `show ip route` (`D` routes with AD 90), Neighbor Adjacency |
| [**`02-dynamic-routing-multi-area-ospf`**](./02-dynamic-routing-multi-area-ospf) | Hierarchical OSPF Backbone | Multi-Area OSPFv2 (Area 0 & 1), ABR Routing | 2x Cisco 2811 | Type-3 Summary LSAs (`O IA` routes with AD 110, Cost 65) |
| [**`03-multi-router-wan-mesh-ecmp`**](./03-multi-router-wan-mesh-ecmp) | 5-Node Full-Mesh WAN ($K_5$) | RIP, Equal-Cost Multi-Path (ECMP), 10 Circuits | 5x Cisco 1841 | Symmetrical dual-path load balancing in RIB |
| [**`04-multi-hop-static-routing`**](./04-multi-hop-static-routing) | Multi-Hop Linear Transit WAN | Next-Hop Static Routing, Symmetrical Return | 3x Cisco 1841 | Recursive routing table lookup, Transit hub forwarding |
| [**`05-hsrp-gateway-redundancy`**](./05-hsrp-gateway-redundancy) | Dual-Segment High Availability | HSRPv2 (Groups 1 & 2), VIPs, Preemption | 2x Cisco 2911 | Active/Standby state failover, Symmetrical return paths |

---

## 🛠️ Core Engineering Highlights

```text
                                  ┌────────────────────────┐
                                  │  Backbone Area 0 (WAN) │
                                  └───────────┬────────────┘
                                              │
                    ┌─────────────────────────┴─────────────────────────┐
                    ▼                                                   ▼
       ┌─────────────────────────┐                         ┌─────────────────────────┐
       │   Primary Gateway (R2)  │ <====== HSRP v2 ======> │   Backup Gateway (R3)   │
       │ Priority 110 (Active)   │   (Virtual IP: 10.1.1.1)│ Priority 100 (Standby)  │
       └────────────┬────────────┘                         └────────────┬────────────┘
                    │                                                   │
                    └─────────────────────────┬─────────────────────────┘
                                              ▼
                                 [ Internal LAN Subnet ]
                                 (10.1.1.0/24 Workstations)
```

1. **Dynamic Routing Mastery:** Validated both Distance-Vector (EIGRP DUAL) and Link-State (OSPF Dijkstra SPF) protocols across multi-area enterprise boundaries.
2. **First-Hop Redundancy (FHRP):** Configured dual-group HSRP v2 to eliminate default gateway failure points for inside clients and outside return traffic.
3. **High-Density WAN Mesh:** Designed a complete graph WAN topology ($K_5$) proving Equal-Cost Multi-Path (ECMP) load distribution across 10 redundant serial links.
4. **Deterministic Static Routing:** Deployed next-hop IP static routes across multi-hop transit paths to ensure recursive lookups without broadcast ARP flooding.

---

## 🧰 Master Routing CLI Verification Cheat Sheet

| Diagnostic Objective | Cisco IOS Command | Expected Operational Output |
| :--- | :--- | :--- |
| **View Routing Table** | `show ip route` | Displays all active Connected (`C`), Static (`S`), EIGRP (`D`), and OSPF (`O`) routes. |
| **Inspect OSPF Neighbors** | `show ip ospf neighbor` | Verifies neighbor states (`FULL/DR`, `FULL/BDR`, `FULL/DROTHER`). |
| **Inspect EIGRP Neighbors** | `show ip eigrp neighbors` | Displays active EIGRP peers, hold times, and smooth round-trip times (SRTT). |
| **Verify HSRP Summary** | `show standby brief` | Displays Active router, Standby router, Priority, Preemption, and Virtual IP. |
| **Inspect Active Interfaces**| `show ip interface brief` | Quick status check ensuring physical Layer 1/2 interfaces are `Up/Up`. |
| **Real-Time Routing Trace** | `traceroute <destination>` | Displays intermediate Layer 3 hops to verify traffic transit paths. |

---

## 📂 Repository File Structure

```text
enterprise-routing-labs/
├── README.md                                  <-- Master Repository Index
├── 01-dynamic-routing-eigrp/
│   ├── README.md
│   ├── topology.png
│   ├── dynamic-routing-eigrp.pkt
│   ├── lhr-router-config.ios
│   └── khi-router-config.ios
├── 02-dynamic-routing-multi-area-ospf/
│   ├── README.md
│   ├── topology.png
│   ├── dynamic-routing-multi-area-ospf.pkt
│   ├── lhr-area0-config.ios
│   └── khi-abr-config.ios
├── 03-multi-router-wan-mesh-ecmp/
│   ├── README.md
│   ├── topology.png
│   ├── multi-router-full-mesh-ecmp.pkt
│   └── configs/ (r0 to r4 router configs)
├── 04-multi-hop-static-routing/
│   ├── README.md
│   ├── topology.png
│   ├── multi-hop-static-routing.pkt
│   └── configs/ (r0 to r2 router configs)
└── 05-hsrp-gateway-redundancy/
    ├── README.md
    ├── topology.png
    ├── hsrp-gateway-redundancy.pkt
    ├── router2-active-config.ios
    └── router3-standby-config.ios
