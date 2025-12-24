# Project Proposal

## Title
Zero Trust Micro-Segmentation for Enterprise & IoT Networks using VMware NSX

## Problem Statement
Flat internal networks allow attackers to move laterally after initial compromise. IoT increases the attack surface
and often lacks strong internal controls. Traditional perimeter security is insufficient.

## Aim
Design, implement, and evaluate a Zero Trust micro-segmentation architecture using VMware NSX to limit east-west
movement and reduce blast radius across enterprise workloads and an IoT-like zone.


## Objectives
1. Build a realistic enterprise and IoT lab topology using VMware vSphere and NSX  
2. Implement NSX Distributed Firewall (DFW) micro-segmentation based on least-privilege principles  
3. Introduce a quarantine model for compromised or high-risk workloads  
4. Simulate lateral movement attacks and compare baseline vs segmented network states  
5. Measure containment effectiveness, allowed flows, and operational impact  


## Research Questions
- How effectively does NSX micro-segmentation reduce lateral movement in mixed enterprise and IoT zones?
- What trade-offs exist between security enforcement and operational complexity?
- Which policy abstraction model (tag-based vs group-based) offers better long-term maintainability?


## Expected Outcomes
- A repeatable and scalable NSX micro-segmentation policy framework  
- An evidence-based evaluation report with metrics, logs, and test results  
- Practical implementation guidelines for adopting Zero Trust micro-segmentation in enterprise environments
