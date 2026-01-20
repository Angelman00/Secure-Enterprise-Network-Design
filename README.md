# Secure Enterprise Network – Multi-Layer Design with DMZ, Redundancy & VoIP

## Overview

This project demonstrates a **security-focused enterprise network design** implemented in Cisco Packet Tracer.
The main goal was to build a **resilient, segmented, and scalable network** using industry best practices, with a strong emphasis on **security, redundancy, and operational clarity** rather than end-user convenience.

The design includes:

* Redundant core infrastructure
* A dedicated DMZ
* Internal server segmentation
* VoIP integration
* Centralized wireless management
* Dynamic routing and firewall-based security enforcement

<img width="1714" height="899" alt="Projekt_Topo" src="https://github.com/user-attachments/assets/02bb7168-e3dc-4272-b15a-e9da27c319fe" />
--

## Network Architecture

### Design Model

* **Hierarchical Design**

  * Core / Distribution: Redundant Multilayer Switches
  * Access Layer: Department-based access switches
* **Firewall-Centric Security Model**
* **Multi-homed Internet connectivity**

### Key Concepts Used

* VLAN-based segmentation
* HSRP for gateway redundancy
* LACP EtherChannel between core switches
* OSPF as the dynamic routing protocol
* Stateful firewall inspection with NAT
* Separate zones for INSIDE, DMZ, and OUTSIDE

---

## VLAN & IP Design

| VLAN | Purpose             | Subnet          |
| ---- | ------------------- | --------------- |
| 10   | Management          | 192.168.10.0/24 |
| 20   | User LAN            | 172.16.0.0/16   |
| 50   | WLAN                | 10.20.0.0/16    |
| 70   | VoIP                | 172.30.0.0/16   |
| 90   | Inside Servers      | 10.11.11.32/27  |
| 199  | Blackhole / Parking | Not routed      |

Unused ports are assigned to a **Blackhole VLAN** and administratively shut down.

---

## Switching & Layer 2 Security

### Access & Server Switches

* PortFast enabled on access ports
* BPDU Guard enabled to protect against rogue switches
* SSH-only management access
* VTY access restricted via ACL
* Native VLAN set to an unused VLAN (891)

### EtherChannel

* LACP used between core multilayer switches
* Active/Passive configuration for stability

---

## Layer 3 & Redundancy

### HSRP

* Implemented on all user-facing VLAN interfaces
* Virtual IP acts as default gateway for endpoints
* Ensures uninterrupted connectivity during failover

### Routing

* **OSPF Area 0** used across:

  * Core switches
  * Firewalls
  * ISP routers
* Loop-free, scalable routing with fast convergence

---

## Firewall Design

### Zones & Security Levels

* INSIDE (Security Level 100)
* DMZ (Security Level 70)
* OUTSIDE (Security Level 0)

### NAT

* Dynamic PAT for:

  * LAN users
  * WLAN users
  * DMZ servers
* Dual-ISP NAT for redundancy

### Access Control

* Explicit inspection policies
* Controlled ICMP, DNS, and HTTP access
* Separate policies per interface

---

## DMZ & Server Infrastructure

### DMZ

* Hosts public-facing services (FTP, Application Server)
* Restricted access enforced by firewall ACLs
* Separate subnet and security zone

### Inside Servers

* DHCP
* DNS
* RADIUS
* Static IP addressing
* Routed via HSRP virtual gateway

---

## Wireless Infrastructure

* Centralized **Wireless LAN Controller**
* Multiple WLANs:

  * Corporate
  * Auditors
  * Guest
* WPA/WPA2 security
* DHCP-based client addressing
* Lightweight AP deployment

---

## VoIP Implementation

* Dedicated Voice VLAN
* Voice Gateway Router with:

  * DHCP Option 150
  * CME Telephony Service
* Auto-assigned extensions
* End-to-end voice segmentation from data traffic

---

## Verification & Testing

Successful validation included:

* Inter-VLAN communication
* Internet access via both ISPs
* DMZ server reachability
* OSPF neighbor adjacencies
* HSRP failover testing
* Wireless client authentication
* VoIP call functionality

---

## Summary

This project reflects a **realistic enterprise-grade network**, combining **high availability, security best practices, and operational structure**.
It is designed as a **learning and demonstration environment** for advanced switching, routing, firewalling, wireless, and VoIP concepts.

---

## Files Included

* Packet Tracer topology
* Device configurations
* Network documentation (this README)

---

**Author:**
Networking Project – Security-Focused Enterprise Design
