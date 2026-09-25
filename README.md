<div align="center">

# 🌐 Enterprise Routing & WAN Architecture Laboratories

[![Infrastructure](https://img.shields.io/badge/Infrastructure-Enterprise_Routing_&_WAN-00599C?style=for-the-badge&logo=cisco&logoColor=white)](https://github.com/abdulwahabsaim)
[![Certification](https://img.shields.io/badge/Certification-Cisco_CCNA_200--301-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)](https://cisco.com)
[![Verified Labs](https://img.shields.io/badge/Verified_Labs-13_Production_Scenarios-brightgreen?style=for-the-badge)]()
[![Location](https://img.shields.io/badge/Location-Netherlands_🇳🇱-orange?style=for-the-badge)]()
[![Author](https://img.shields.io/badge/Author-Abdul_Wahab_Saim-blueviolet?style=for-the-badge)](https://linkedin.com/in/abdulwahabsaim)

<p align="center">
  <b>A comprehensive, production-grade repository of 13 hands-on enterprise routing, WAN redundancy, IPv6 dual-stack, traffic shaping, and site-to-site overlay labs designed for Level 1 / Level 2 Network Operations Center (NOC) and Infrastructure roles.</b>
</p>

[Core Domains](#-core-technical-domains) • [Skills Matrix](#-topics--skills-coverage-matrix) • [Detailed Lab Directory](#-detailed-laboratory-catalog-13-scenarios) • [Protocol Reference](#-enterprise-routing-protocol-matrix) • [NOC Runbook](#-enterprise-routing-cli-runbook)

</div>

---

## 📌 Executive Summary

Modern enterprise networks demand deterministic packet forwarding, sub-second failover convergence, protocol-level traffic prioritization, and secure boundary translation. This repository documents a systematic collection of **13 production-style routing labs** designed and verified in Cisco Packet Tracer and GNS3.

Every lab adheres to strict enterprise design principles:
* **Separation of Planes:** Clear demarcation between Layer 2 switching domains, Layer 3 internal routing fabrics, and WAN boundary interfaces.
* **Resilient Path Selection:** Active-Active distribution routing, Administrative Distance (AD) failover, and Unequal-Cost Load Balancing (UCLB).
* **Deterministic Verification:** Comprehensive CLI proof tables (`show ip route`, `show ip ospf neighbor`, `show ip eigrp topology`, `show ip nat translations`, `show policy-map interface`).
* **Zero Tutorial Clutter:** Every lab directory contains clean, paste-ready `.ios` configurations with explicit interface descriptions and `no shutdown` statements.

---

## 🧱 Core Technical Domains

```text
                               ┌──────────────────────────────────────────────────────────┐
                               │       ENTERPRISE ROUTING & WAN INFRASTRUCTURE            │
                               └────────────────────────────┬─────────────────────────────┘
                                                            │
         ┌──────────────────────────┬───────────────────────┴───────────────┬──────────────────────────┐
         │                          │                                       │                          │
         ▼                          ▼                                       ▼                          ▼
┌──────────────────┐      ┌────────────────────┐                 ┌────────────────────┐      ┌────────────────────┐
│  DYNAMIC IGPs    │      │  WAN & TRANSIT     │                 │ CAMPUS CORE & L3   │      │ EDGE SERVICES &    │
│  (OSPF & EIGRP)  │      │  TOPOLOGIES        │                 │ REDUNDANCY         │      │ OVERLAYS           │
├──────────────────┤      ├────────────────────┤                 ├────────────────────┤      ├────────────────────┤
│• Multi-Area OSPF │      │• 5-Node Full Mesh  │                 │• Multilayer SVIs   │      │• Dynamic PAT / NAT │
│• Type-3 LSAs/ABR │      │• ECMP (10 Links)   │                 │• L3 Routed Uplinks │      │• IPv6 GUA & SLAAC  │
│• Timers & P2P/Bcast     │• Multi-Hop Static  │                 │• Dual-Group HSRPv2 │      │• Link-Local Fe80:: │
│• DUAL Algorithm  │      │• Symmetrical Returns                 │• Preemption Tuning │      │• Modular QoS (MQC) │
│• Variance (UCLB) │      │• Recursive Routing │                 │• Active-Active VIPs│      │• GRE VPN Overlays  │
└──────────────────┘      └────────────────────┘                 └────────────────────┘      └────────────────────┘
```

---

## 🎯 Topics & Skills Coverage Matrix

Use this matrix to locate specific protocols, commands, and operational scenarios across the 13 laboratories:

| Technical Topic / Competency | Primary Protocol / Feature | Implemented In | Key Cisco IOS Commands |
| :--- | :--- | :--- | :--- |
| **Distance-Vector Dynamic Routing** | EIGRP AS 7 | [Lab 01](./01-dynamic-routing-eigrp/) | `router eigrp 7`, `no auto-summary`, `network` |
| **Hierarchical Link-State Routing** | Multi-Area OSPFv2 | [Lab 02](./02-dynamic-routing-multi-area-ospf/) | `router ospf 1`, `network [ip] [wildcard] area [id]` |
| **Equal-Cost Multi-Path (ECMP)** | Full-Mesh ($K_5$) WAN | [Lab 03](./03-multi-router-wan-mesh-ecmp/) | `ip route`, `show ip route` (multi-path metrics) |
| **Multi-Hop Transit Forwarding** | Next-Hop Static Routing | [Lab 04](./04-multi-hop-static-routing/) | `ip route [dest] [mask] [next-hop-ip]` |
| **First Hop Gateway Redundancy** | Dual-Segment HSRPv2 | [Lab 05](./05-hsrp-gateway-redundancy/) | `standby version 2`, `standby [grp] priority`, `preempt` |
| **Wire-Speed Inter-VLAN Routing** | Multilayer Switch SVIs | [Lab 06](./06-intervlan-routing-multilayer-svi/) | `ip routing`, `interface Vlan[id]`, `no switchport` |
| **Administrative Distance Tuning** | Floating Static Routes | [Lab 07](./07-floating-static-routes-wan-failover/) | `ip route [dest] [mask] [next-hop] 120` |
| **OSPF Adjacency Troubleshooting** | Timers & Network Types | [Lab 08](./08-ospf-neighbor-troubleshooting-lsdb/) | `ip ospf hello-interval`, `ip ospf network point-to-point` |
| **Next-Gen IPv6 Routing & SLAAC** | Dual-Stack & Link-Local | [Lab 09](./09-ipv6-dual-stack-routing-slaac/) | `ipv6 unicast-routing`, `ipv6 enable`, `ipv6 route` |
| **IPv4 Address Exhaustion Defense**| Dynamic PAT (Overload) | [Lab 10](./10-enterprise-edge-nat-pat-overload/) | `ip nat inside`, `ip nat outside`, `ip nat inside source` |
| **Traffic Shaping & Prioritization**| Modular QoS CLI (MQC) | [Lab 11](./11-modular-qos-traffic-prioritization/) | `class-map`, `policy-map`, `priority percent`, `set ip dscp` |
| **Site-to-Site Encapsulation** | Point-to-Point GRE | [Lab 12](./12-site-to-site-gre-tunnel-ospf/) | `interface Tunnel0`, `tunnel source`, `tunnel destination` |
| **Unequal-Cost Load Balancing** | DUAL Feasibility & Variance | [Lab 13](./13-dynamic-routing-eigrp-variance/) | `variance 2`, `show ip eigrp topology` |

---

## 🗺️ Detailed Laboratory Catalog (13 Scenarios)

### 🔹 [01-dynamic-routing-eigrp](./01-dynamic-routing-eigrp/)
* **Focus:** EIGRP AS 7 Dynamic Routing & Composite Metric Mechanics
* **Hardware:** 2x Cisco 2811 Routers (LHR & KHI Branches)
* **Key Topics Covered:** EIGRP autonomous systems, DUAL finite state machine, bandwidth/delay composite metric computation, classless subnet advertisements over Point-to-Point Serial WAN circuits, and bidirectional route verification.

### 🔹 [02-dynamic-routing-multi-area-ospf](./02-dynamic-routing-multi-area-ospf/)
* **Focus:** Hierarchical Link-State Design & Area Border Routers (ABR)
* **Hardware:** 2x Cisco 2811 Routers
* **Key Topics Covered:** OSPF hierarchy (Backbone Area 0 vs Standard Area 1), ABR role mechanics, Type-3 Summary LSA generation, SPF tree calculation, and multi-area routing table propagation.

### 🔹 [03-multi-router-wan-mesh-ecmp](./03-multi-router-wan-mesh-ecmp/)
* **Focus:** 5-Node Complete Graph ($K_5$) Full-Mesh WAN & ECMP
* **Hardware:** 5x Cisco 1841 Routers (10 Interconnecting Serial Links)
* **Key Topics Covered:** Full-mesh WAN topologies, Equal-Cost Multi-Path (ECMP) load balancing across parallel links, dynamic link metrics, routing table multi-hop convergence, and transit path redundancy.

### 🔹 [04-multi-hop-static-routing](./04-multi-hop-static-routing/)
* **Focus:** Multi-Hop Transit Forwarding & Recursive Routing Tables
* **Hardware:** 3x Cisco 1841 Routers (Linear Transit WAN)
* **Key Topics Covered:** Next-hop IP vs exit-interface static routing, recursive routing table lookups, symmetrical return path configuration, and resolving asymmetric routing blackholes.

### 🔹 [05-hsrp-gateway-redundancy](./05-hsrp-gateway-redundancy/)
* **Focus:** Dual-Segment First Hop Redundancy Protocol (HSRPv2)
* **Hardware:** 2x Cisco 2911 Routers, 2x Catalyst 3650 Multilayer Switches
* **Key Topics Covered:** HSRPv2 active/standby election, Virtual IP (VIP) and virtual MAC binding (`0000.0C9F.Fxxx`), priority manipulation, preemption configuration, and synchronized bidirectional failover across inside LAN and outside WAN transit segments.

### 🔹 [06-intervlan-routing-multilayer-svi](./06-intervlan-routing-multilayer-svi/)
* **Focus:** Multilayer Campus Switching, SVIs & Routed Uplinks
* **Hardware:** Catalyst 3650 Multilayer Switch, Cisco 2911 Edge Router, Catalyst 2960
* **Key Topics Covered:** Migrating legacy Router-on-a-Stick (ROAS) to wire-speed Multilayer Switching, creating Switch Virtual Interfaces (SVIs), enabling global `ip routing`, provisioning point-to-point Layer 3 routed interfaces (`no switchport`), and default gateway routing.

### 🔹 [07-floating-static-routes-wan-failover](./07-floating-static-routes-wan-failover/)
* **Focus:** Administrative Distance (AD) Manipulation & Dual-ISP Failover
* **Hardware:** 2x Cisco 2911 Routers, 2x ISP Edge Nodes
* **Key Topics Covered:** Administrative Distance hierarchy (OSPF AD 110 vs Static AD 120), configuring floating static backup routes, simulating primary link failure, observing automated routing table re-convergence, and symmetrical return path failover.

### 🔹 [08-ospf-neighbor-troubleshooting-lsdb](./08-ospf-neighbor-troubleshooting-lsdb/)
* **Focus:** OSPF Neighbor Adjacency Troubleshooting & Link-State Database (LSDB)
* **Hardware:** 4x Cisco 2911 Routers (Complex Mesh)
* **Key Topics Covered:** Resolving common OSPF failure states: Hello/Dead timer mismatches, OSPF Network Type mismatches (`point-to-point` vs `broadcast`), MTU issues, serial clock rates, default route injection (`default-information originate`), and inspecting Type 1 (Router) vs Type 2 (Network) LSAs.

### 🔹 [09-ipv6-dual-stack-routing-slaac](./09-ipv6-dual-stack-routing-slaac/)
* **Focus:** IPv6 Static Routing, SLAAC Host Autoconfiguration & Link-Local Next Hops
* **Hardware:** 3x Cisco 2911 Routers
* **Key Topics Covered:** Global Unicast Addresses (GUA) vs Link-Local Addresses (LLA), enabling `ipv6 unicast-routing`, Stateless Address Autoconfiguration (SLAAC) via ICMPv6 Router Advertisements, routing across pure `FE80::` link-local transit interfaces (`ipv6 enable`), and fully-specified IPv6 floating static backup routes.

### 🔹 [10-enterprise-edge-nat-pat-overload](./10-enterprise-edge-nat-pat-overload/)
* **Focus:** Enterprise Edge NAT & Dynamic Port Address Translation (PAT)
* **Hardware:** Cisco 2911 Edge Router, Internet Gateway
* **Key Topics Covered:** Solving private IPv4 (RFC 1918) address exhaustion, defining `ip nat inside` and `ip nat outside` boundaries, Access Control List interesting traffic matching, PAT (NAT Overload) Layer 4 port multiplexing, and analyzing active translation sessions via `show ip nat translations`.

### 🔹 [11-modular-qos-traffic-prioritization](./11-modular-qos-traffic-prioritization/)
* **Focus:** Modular QoS CLI (MQC), DSCP Marking & Low Latency Queuing (LLQ)
* **Hardware:** Cisco 4331 ISR Router
* **Key Topics Covered:** The 3-step MQC architecture: Classification (`class-map` with NBAR deep protocol inspection), Marking (`policy-map` with DSCP AF31, AF32, and CS2), and Scheduling (`service-policy output` allocating LLQ strict priority for latency-sensitive traffic and CBWFQ bandwidth for web/data).

### 🔹 [12-site-to-site-gre-tunnel-ospf](./12-site-to-site-gre-tunnel-ospf/)
* **Focus:** Generic Routing Encapsulation (GRE) Site-to-Site VPN & OSPF Overlay
* **Hardware:** 2x Cisco 2911 Branch Routers, Untrusted ISP Backbone
* **Key Topics Covered:** Overlay vs underlay network concepts, virtual `Tunnel0` interface configuration, tunnel source/destination endpoints, adjusting IP MTU (`mtu 1476`) to prevent packet fragmentation, and dynamically routing private branch subnets across public networks using an OSPF overlay.

### 🔹 [13-dynamic-routing-eigrp-variance](./13-dynamic-routing-eigrp-variance/)
* **Focus:** DUAL Feasibility Condition & Unequal-Cost Multi-Path (UCMP) Load Balancing
* **Hardware:** 4x Cisco 2911 Routers (Diamond Topology)
* **Key Topics Covered:** Mathematical proof of the Feasibility Condition ($AD < FD$), identifying Successors vs Feasible Successors in the topology table, tuning the `variance 2` multiplier to install asymmetric metric routes into the RIB, and distributing traffic proportionally across unequal link speeds (Gigabit vs FastEthernet).

---

## 📊 Enterprise Routing Protocol Matrix

A quick-reference architectural comparison of the protocols and mechanisms implemented across this repository:

| Feature / Protocol | Default Admin Distance (AD) | Metric Calculation Mechanism | Convergence Speed | Multi-Path Capability | Standard RFC / Spec |
| :--- | :---: | :--- | :---: | :---: | :--- |
| **Directly Connected** | `0` | Physical / Data Link state | Instantaneous | N/A | IEEE 802.3 |
| **Static Route** | `1` | Configured next-hop / interface | Instantaneous | ECMP | Cisco IOS Standard |
| **Floating Static** | Tuned (`120`) | AD priority manipulation | Upon Primary Down | Failover Standby | Cisco IOS Standard |
| **EIGRP (Internal)** | `90` | Bandwidth + Delay (Composite) | Sub-second (DUAL) | **ECMP + UCLB (`variance`)** | RFC 7868 |
| **OSPFv2 / OSPFv3** | `110` | Cost = $\frac{\text{Reference Bandwidth}}{\text{Interface Bandwidth}}$ | Rapid (Dijkstra SPF) | ECMP (Up to 16/32 paths)| RFC 2328 / RFC 5340 |
| **HSRPv2 (FHRP)** | N/A | Priority (`100` default) + Preempt | 3s Hello / 10s Hold | Active / Standby VIP | RFC 2281 |
| **GRE Encapsulation**| N/A | Virtual point-to-point overlay | Bound to Underlay | Dynamic Overlay Routing | RFC 2784 / RFC 2890 |

---

## 🧰 Enterprise Routing CLI Runbook

Essential Cisco IOS diagnostic commands demonstrated and documented across these 13 laboratories:

```text
================================================================================
CATEGORY 1: ROUTING TABLE & FORWARDING INSPECTION
================================================================================
show ip route                         # Displays the active Global Routing Information Base (RIB)
show ip route [subnet]                # Displays detailed administrative distance, metric, and next-hop
show ip route ospf                    # Filters routing table strictly for OSPF-learned prefixes
show ip route eigrp                   # Filters routing table strictly for EIGRP-learned prefixes
show ipv6 route                       # Displays active IPv6 routing table and next-hop GUAs/LLAs

================================================================================
CATEGORY 2: DYNAMIC PROTOCOL ADJACENCIES & LSDB
================================================================================
show ip ospf neighbor                 # Validates OSPF neighbor states (INIT, 2-WAY, EXSTART, FULL)
show ip ospf database                 # Displays the Link-State Database (Type 1 Router, Type 2 Network LSAs)
show ip ospf interface [id]           # Inspects Hello/Dead timers, network type (P2P/Broadcast), and DR/BDR role
show ip eigrp neighbors               # Displays active EIGRP peers, hold times, and queue counters
show ip eigrp topology                # Displays Successors and Feasible Successors meeting the Feasibility Condition
show ip eigrp topology all-links      # Displays all known paths including non-feasible backups

================================================================================
CATEGORY 3: EDGE SERVICES, TELEMETRY & OVERLAYS
================================================================================
show standby brief                    # Displays HSRP active/standby state, configured priority, and VIP
show ip nat translations              # Displays active dynamic NAT / PAT Layer 4 multiplexing sessions
show ip nat statistics                # Displays total translation hits, misses, and inside/outside interfaces
show policy-map interface [id]        # Displays real-time QoS class matching, DSCP marking, and drop counters
show interface Tunnel [id]            # Verifies GRE tunnel line protocol, source, destination, and transport MTU
```

---

## 📁 Standardized 4-File Package Structure

To maintain production standards, every lab subfolder in this repository is strictly organized as a self-contained 4-file unit:

```text
0X-lab-topic-name/
├── README.md                      # In-depth technical documentation, schema tables & CLI proof
├── topology.png                   # Clean, 16:9 cropped enterprise topology diagram
├── <lab-name>.pkt                 # Completed, verified Cisco Packet Tracer simulation file
└── <device>-config.ios            # Syntax-highlighted, clean running configurations (paste-ready)
```

---

## 👤 Profile
* **Candidate:** Abdul Wahab Saim
* **Primary Certification:** Cisco Certified Network Associate (CCNA 200-301)
* **Professional Links:**
  * **GitHub:** [github.com/abdulwahabsaim](https://github.com/abdulwahabsaim)
  * **Live Portfolio Website:** [abdulwahabsaim.github.io](https://abdulwahabsaim.github.io)
  * **LinkedIn:** [linkedin.com/in/abdulwahabsaim](https://www.linkedin.com/in/abdulwahabsaim/)

---
