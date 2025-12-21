# Zero Trust Micro-Segmentation for Enterprise & IoT Networks using VMware NSX

This repository contains an MSc-level applied cybersecurity project that designs, implements, and evaluates
a **Zero Trust micro-segmentation architecture** using **VMware NSX Distributed Firewall (DFW)** to prevent
lateral movement attacks across **enterprise workloads** and an **IoT-like zone**.

## Goals
- Implement **least-privilege** east-west traffic control using NSX DFW
- Build an **enterprise + IoT** lab topology with clear security zones
- Compare security posture **before vs after** micro-segmentation
- Simulate attack paths (lateral movement) and measure containment outcomes

## Tech Stack
- VMware vSphere (lab)
- VMware NSX (DFW, Segments, Groups, Policies)
- Linux & Windows VMs
- Basic attacker VM (Kali or equivalent) for simulation
- tcpdump/Wireshark for traffic analysis

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
This project is designed for **authorized lab use only**. Do not run attack simulations on production networks.
