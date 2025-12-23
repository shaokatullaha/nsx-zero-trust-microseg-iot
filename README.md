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

## Lab Topology (High Level)
Zones:
- User Zone (jumpbox / admin)
- App Zone (web/app)
- DB Zone (database)
- IoT Zone (simulated IoT services)
- Management Zone (vCenter/NSX managers)

## Repository Guide
- `docs/` – proposal, architecture, threat model, evaluation
- `lab/` – IP plan, segments, NSX objects and policies, runbooks
- `scripts/` – traffic generators, simulation helpers, log collectors
- `results/` – baseline vs micro-segmentation evidence & report template

## How to Use (Suggested Order)
1. Read `docs/project-proposal.md`
2. Build the lab from `lab/topology/*`
3. Create NSX objects in `lab/nsx/objects/*`
4. Apply baseline policy: `lab/nsx/policies/baseline-allowlist.md`
5. Capture baseline results in `results/baseline/`
6. Apply micro-segmentation policies
7. Execute validation from `lab/validation/attack-scenarios.md`
8. Record results in `results/microseg-enabled/`
9. Complete `results/report-template.md`

## Disclaimer
This project is intended exclusively **only for authorized laboratory environments**.
No attack simulations should be performed on production networks.