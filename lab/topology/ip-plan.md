# IP Plan 

## Management / NSX Components 
- DNS server 10.5.50.2
- vCenter Server: 10.5.50.5
- ESXi mgmt: 10.5.50.11-14
- NSX Cluster: 10.5.50.20
- NSX Manager: 10.5.50.15-17
- Edge nodes: 10.5.50.18-19

## Workload Segments
- USER-Segment: 10.50.10.0/24
- Web-Segment:  10.50.20.0/24 
- APP-Segment:  10.50.30.0/24
- DB-Segment:   10.50.40.0/24
- IoT-Segment:  10.50.50.0/24

## Gateways
- T1-ZT (Tier-1): 10.10.10.1, 10.10.20.1, 10.10.30.1, 10.10.40.1
- T0-EDGE (Tier-0): Upstream to home lab router (optional)

## Notes
- Use NAT if you want internet access for VMs.
- Keep NSX Manager access restricted (mgmt only).
