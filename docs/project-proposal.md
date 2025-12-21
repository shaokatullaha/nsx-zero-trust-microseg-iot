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
1. Build an enterprise + IoT lab topology
2. Implement NSX DFW micro-segmentation with least privilege
3. Introduce a quarantine model for compromised workloads
4. Simulate lateral movement and compare baseline vs segmented states
5. Measure containment, allowed flows, and operational impact

## Research Questions
- How effectively does NSX micro-segmentation reduce lateral movement in mixed enterprise + IoT zones?
- What is the trade-off between security and operational complexity?
- Which policy model (tag-based vs group-based) is most maintainable?

## Expected Outcomes
- A repeatable NSX policy framework
- Evidence-based evaluation report with metrics and test results
- Practical guidelines for adopting Zero Trust micro-segmentation
