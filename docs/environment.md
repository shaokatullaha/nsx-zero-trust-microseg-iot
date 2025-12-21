# Lab Environment

## Platform Versions
- VMware ESXi: 8.0.3 (4 hosts)
- VMware vCenter: 8.0.3
- VMware NSX: 4.2.x (Standalone)
- Switching: vSphere Distributed Switch (VDS)

## Physical/Logical Layout
- 4-node ESXi cluster
- Workloads connected to NSX Segments (Overlay)
- DFW (Distributed Firewall) used for micro-segmentation
- Tier-1 gateway provides routing between segments (Tier-0 optional)

## Notes
- All attack simulations and testing are performed ONLY in an isolated lab.
