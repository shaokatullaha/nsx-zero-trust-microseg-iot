# IP Plan 

## Management / NSX-T Components (example)
- NSX Manager: 10.10.0.10
- vCenter (if used): 10.10.0.11
- ESXi mgmt: 10.10.0.20-30

## Workload Segments
- SEG-USER: 10.10.10.0/24
- SEG-APP:  10.10.20.0/24
- SEG-DB:   10.10.30.0/24
- SEG-IOT:  10.10.40.0/24

## Gateways
- T1-ZT (Tier-1): 10.10.10.1, 10.10.20.1, 10.10.30.1, 10.10.40.1
- T0-EDGE (Tier-0): Upstream to home lab router (optional)

## Notes
- Use NAT if you want internet access for VMs.
- Keep NSX Manager access restricted (mgmt only).
