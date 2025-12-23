# Zero Trust Micro-Segmentation for Enterprise & IoT Networks using VMware NSX

## Overview

This project presents an **applied Zero Trust security architecture** implemented using **VMware NSX Distributed Firewall (DFW)** to protect **enterprise workloads and IoT devices** from lateral movement attacks.

The work demonstrates how **default-deny east-west controls, identity-driven policy enforcement**, and **continuous verification** significantly improve internal network security compared to traditional flat network designs.

The project is implemented in a **real VMware NSX lab**, validated through **attack simulation**, and supported by **measurable before/after security evidence**, making it suitable for both **MSc Cybersecurity evaluation** and **real-world enterprise security reference.**

## Problem Statement

Modern enterprise networks increasingly include **IoT devices** alongside critical application workloads.
In flat or perimeter-focused network designs, a single compromised device can enable **unrestricted lateral movement**, leading to ransomware spread, data breaches, or service disruption.

This project addresses the question:

"How effectively can Zero Trust micro-segmentation reduce lateral movement risk across enterprise and IoT workloads in a realistic network environment?"

## Project Objectives
- Enforce **default-deny east-west traffic control**
- Apply **least-privilege access** using dynamic, identity-based policies
- Isolate IoT devices to **only required services**
- Compare **security posture before vs. after micro-segmentation**
- Validate effectiveness through **controlled attack simulations**

## High-Level Architecture

<p align="center">
  <img src="" width="800">
</p>
<p align="center">
  <img src="" width="800">
</p>
<p align="center">
  <img src="" width="800">
</p>

## Security Zones
- **MGMT** – vCenter, NSX Manager, jump host, logging
- **SHARED** – DNS, NTP, authentication services
- **APP-TIER** – Web and application services
- **DB-TIER** – Databases
- **IoT-ZONE** – Simulated IoT devices (CCTV, sensors, controllers)
- **(Optional) USER-ZONE** – Admin or user access systems

- `scripts/` – traffic generators, simulation helpers, log collectors


## Core Zero Trust Principles
- No implicit trust based on network location
- Explicit allow rules for required application flows only
- IoT devices restricted to minimum necessary communication
- Continuous verification via firewall rule enforcement and logging

## Technology Stack
- VMware vSphere (ESXi lab environment)
- VMware NSX (Distributed Firewall, Segments, Groups, Policies)
- Linux and Windows virtual machines
- Simulated IoT workloads (Linux-based services)
- Attacker VM (Kali Linux or equivalent)
- Traffic analysis tools (tcpdump, Wireshark)

## Security Design & Policy Model

- **Tag-based workload identity** (e.g., zone:app, role:web, zone:iot)
- **Dynamic groups** derived from metadata, not IP addresses
- **Distributed Firewall (DFW)** enforcing east-west controls at the vNIC level
- Centralized policy logic with decentralized enforcement

## Example Allowed Flows

- Web → API (TCP 443)
- API → Database (TCP 3306 / 1433)
- Any → DNS (TCP/UDP 53, restricted)
- Any → NTP (UDP 123, restricted)
- IoT → IoT Broker / NVR (application-specific)

## Default Rule

- **ANY → ANY : DENY (east-west)** 

## Threat Model & Attack Simulation

This project includes a structured **threat model** aligned with **MITRE ATT&CK**, focusing on:

    - Network discovery
    - Lateral movement
    - Privilege escalation risk

Attack simulations are performed from a **compromised IoT workload**, attempting to:

    - Scan enterprise segments
    - Access application and database services
    - Pivot across security zones

All results are validated using **NSX firewall logs, rule hit counts, and blocked session evidence**.

## Validation Methodology

1. Baseline phase

        - Flat network behavior observed
        - Unrestricted east-west communication verified

2. Zero Trust enforcement phase

        - Micro-segmentation policies applied
        - Application functionality validated

3. Attack simulation phase

        - Unauthorized lateral movement attempts executed
        - All blocked connections documented

## Results Summary

- Significant reduction in permitted east-west traffic
- IoT workloads fully isolated from enterprise application tiers
- 100% block rate for simulated lateral movement attempts
- No disruption to legitimate application flows

Detailed evidence is available in docs/results.md.

## Academic & Professional Relevance

This project is suitable for:

  - MSc Cybersecurity capstone or dissertation work
  - Scholarship and admission portfolio review
  - Enterprise security architecture reference
  - Professional interviews and consulting demonstrations

It demonstrates applied knowledge of:

  - Zero Trust Architecture (ZTA)
  - Network access control
  - Threat containment
  - Security validation and measurement

## Disclaimer
This project is intended exclusively **only for authorized laboratory environments**.
No attack simulations should be performed on production networks.