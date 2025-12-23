# Architecture Design – Zero Trust Micro-Segmentation (VMware NSX)


## 1. Architecture Objective
The objective of this architecture is to implement a practical Zero Trust model using VMware NSX
micro-segmentation to prevent unauthorized east-west traffic and reduce lateral movement risk across
enterprise workloads and an IoT-like zone.

The architecture is designed for **measurable evaluation**, enabling a clear before/after comparison of
allowed flows and blocked attack paths.

## 2. Scope
### In-Scope
- East-west traffic control between security zones using NSX Distributed Firewall (DFW)
- Enterprise application tiers (Web/API/DB)
- Shared infrastructure services (DNS, NTP, authentication optional)
- IoT-zone containment (simulated IoT workloads)
- Evidence collection: rule hits, logs, flow visibility, packet captures

### Out-of-Scope (Explicitly)
- Production-grade PKI/IAM redesign (only minimal identity constructs for lab)
- Full SIEM pipeline (log forwarding optional; local evidence acceptable for evaluation)
- Full north-south perimeter redesign (Gateway Firewall / Edge is optional)

## 3. Logical Security Zones (Security Domains)
The environment is divided into the following security domains:

- **MGMT**: vCenter, NSX Manager, jump host, logging collector
- **SHARED**: DNS, NTP, directory/auth services (optional)
- **APP-TIER**: Web and application services
- **DB-TIER**: Database services
- **IOT-ZONE**: Simulated IoT devices (CCTV/sensors/controllers)
- **USER-ZONE (optional)**: Admin/user access systems (VDI/jump endpoints)

Each zone represents a distinct trust boundary with a controlled set of allowed inter-zone flows.

## 4. Segmentation Strategy

Each security domain is mapped to a dedicated NSX segment (example names):
- SEG-MGMT, SEG-SHARED, SEG-APP, SEG-DB, SEG-IOT

**Default Deny:** East-west traffic between segments is denied by default.
**Explicit Allow:** Only application-justified flows are permitted (e.g., Web→API, API→DB, IoT→DNS/NTP/Broker).

## 5. Policy Enforcement Points

### Primary Enforcement: NSX Distributed Firewall (DFW)
Micro-segmentation is enforced using **DFW at the vNIC level**, providing workload-level control that:
- persists across IP changes
- supports dynamic grouping based on identity metadata
- enables granular allow-only policies for east-west traffic

### Optional Controls (If Available)
- Gateway Firewall for north-south segmentation
- NSX Intelligence for flow discovery and policy recommendations

## 6. Identity and Policy Model (Zero Trust Policy Abstraction)
Policies are defined using **metadata** rather than IP addresses:

- **Tags (examples):**
  - zone:mgmt, zone:shared, zone:app, zone:db, zone:iot
  - role:web, role:api, role:db, iot:type=cctv

- **Dynamic Groups (examples):**
  - GRP_APP_WEB = role:web
  - GRP_APP_API = role:api
  - GRP_DB = role:db
  - GRP_IOT = zone:iot
  - GRP_SHARED_DNS/NTP = zone:shared AND role:dns/ntp

This approach supports scalability and reduces operational risk when workloads are added/moved.

## 7. Traffic Model (Approved Flows)
The design permits only required service flows, for example:
- APP: WEB → API (TCP/443)
- APP: API → DB (TCP/3306 or TCP/1433)
- Infra: Any → DNS (TCP/UDP 53) to approved DNS servers only
- Infra: Any → NTP (UDP 123) to approved NTP servers only
- IoT: IoT → Broker/NVR (required ports only)
All other east-west traffic is denied.

## 8. Telemetry, Logging, and Evidence Collection
Evidence is collected to support a repeatable MSc-level evaluation:
- NSX DFW rule hit counts (proof of enforcement)
- Flow logs / blocked sessions (proof of denial)
- Packet captures (tcpdump/Wireshark) for verification
- Before/after flow comparison (baseline vs microseg-enabled)

Screenshots and evidence are stored in:
- docs/screenshots/
- attacks/evidence/
- results templates in docs/results.md

## 9. Alignment with NIST Zero Trust Principles (Conceptual)
This design aligns with Zero Trust principles by enforcing:
- **Least Privilege:** only explicitly required flows are allowed
- **Continuous Verification:** every flow is evaluated against policy
- **Assume Breach:** compromised IoT/endpoint is contained by segmentation
- **Explicit Trust Decisions:** access is based on identity/context (tags/groups), not network location

<p align="center">
  <img src="diagram/zero-trust-architecture.png" width="800">
</p>

**Figure:** Zero Trust Micro-Segmentation Architecture using VMware NSX
