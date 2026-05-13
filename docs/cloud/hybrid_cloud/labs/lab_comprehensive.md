# Comprehensive Lab: Hybrid Cloud Design & Implementation

This lab consolidates the core concepts, architectural patterns, and practical implementation steps from across the 8 sessions of the Hybrid Cloud course. You will work through a cohesive scenario, moving from strategic assessment to hands-on networking, security, data management, and operational setup.

---

## The Master Scenario: "HealthSync Global"

**Business Context:**
HealthSync Global is a large medical technology company. They maintain highly sensitive patient data on-premises in their private data centers across Europe (due to GDPR and local healthcare regulations). However, they want to modernize their "Patient Insights" platform to leverage public cloud AI/ML tools for early disease detection and provide a global web portal for doctors to access diagnostic summaries.

**High-Level Requirements:**

1. **Privacy:** Patient PII must never leave the on-premises secure zone.
2. **Performance:** Real-time diagnostics require sub-20ms latency.
3. **Availability:** The system must be resilient to cloud or network outages.
4. **Operations:** A unified view of both on-premises and cloud health is mandatory.

---

## Phase 1: Strategic Assessment & Architectural Design

_Related Sessions: [Session 1: Intro](docs/cloud/hybrid_cloud/session1_intro_to_hybrid_cloud.md), [Session 2: Architectures](docs/cloud/hybrid_cloud/session2_architectures_and_models.md)_

### Task 1.1: The Hybrid Matrix

Before building, compare the models to justify the hybrid approach to the board.

1. Create a matrix comparing Public, Private, and Hybrid cloud models based on:
   - **Cost** (CapEx vs OpEx)
   - **Control** (Security/Compliance)
   - **Agility** (Speed of innovation)
2. Identify why a "Pure Public" or "Pure Private" model fails for HealthSync Global's requirements.

### Task 1.2: Pattern Selection & Justification

1. Review the three primary patterns: **Tiered**, **Partitioned**, and **Distributed**.
2. **Design Decision:** Which pattern is best for the "Patient Insights" platform where AI processing happens in the cloud but the "System of Record" (Database) stays on-premises?
3. **Justify:** Explain the impact of **Data Gravity** on your choice. Why wouldn't a fully Distributed (Active-Active) pattern work for the sensitive database?

---

## Phase 2: Hybrid Networking & Connectivity

_Related Sessions: [Session 3: Networking](docs/cloud/hybrid_cloud/session3_networking_strategies.md)_

### Task 2.1: The Universal Overlay (Practical)

Create a secure, encrypted mesh network to connect your "On-Prem" (Local), "Development" (Linode), and "Cloud AI" (GCP/AWS/Azure) environments.

1. **Setup:** Install an overlay network tool (e.g., [Tailscale](https://tailscale.com) or Wireguard) on your local machine and two cloud instances.
2. **Connectivity Check:**

   ```bash
   # Verify the mesh is active
   tailscale status
   ping <other-node-overlay-ip>
   ```

3. **Subnet Routing:** Configure your local machine to advertise its internal subnet so cloud services can reach on-premises legacy devices.

### Task 2.2: Advanced Connectivity Planning

For the production environment (HealthSync Global), a software VPN over the internet is insufficient.

1. **Selection:** Propose a primary connection method (e.g., **Dedicated Interconnect/ExpressRoute**) to meet the sub-20ms latency SLA.
2. **BGP & Redundancy:** Define a routing strategy. If the primary Interconnect fails, how will BGP handle the failover to a backup Site-to-Site VPN?
3. **DNS Resolution:** Configure **Conditional Forwarding**. How will a Cloud VM resolve `mri-database.healthsync.internal`?

---

## Phase 3: Identity & Security

_Related Sessions: [Session 4: IAM](../session4_iam_and_security.md), [Session 7: Security](../session7_security_and_compliance.md)_

### Task 3.1: Unified Identity Workflow

1. **Scenario:** A new Radiologist joins. They are added to the on-premises Active Directory.
2. **Workflow:** Detail the steps (Synchronization vs. Federation) required for them to access the Cloud AI portal using their existing credentials.
3. **Zero Trust Implementation:** Define how you will verify every request. If a user tries to access the patient DB from an unmanaged home laptop, which policy should block it?

### Task 3.2: Security Shared Responsibility

1. Create a table mapping the "Security OF the Cloud" (Provider) vs "Security IN the Cloud" (HealthSync) for a Managed Kubernetes (GKE/AKS) environment.
2. **Encryption:** Propose an encryption strategy for data-at-rest (Local & Cloud) and data-in-transit (MACsec or IPsec over the Interconnect).

---

## Phase 4: Data Management & AI Implementation

_Related Sessions: [Session 5: Data Management](../session5_data_management.md), [Session 8: Implementation](../session8_implementation_and_use_cases.md)_

### Task 4.1: The PII Firewall (Design)

HealthSync cannot send PII to the cloud.

1. **Technical Design:** Design a "Transformation Gateway" on-premises.
2. **Payload:** Provide a sample JSON payload of a medical record (e.g., age, weight, symptoms, location-hash) that is safe for Cloud AI processing but contains no PII (no names, SSNs, or addresses).

### Task 4.2: Hybrid Storage & Backup (Practical)

Implement a **3-2-1 Strategy**: Local (Primary) -> Linode (Warm Backup) -> GCP/Azure/AWS (Archive).

1. **Sync Task:** Use `rclone` to move local diagnostic logs to a cloud object storage bucket.

   ```bash
   rclone sync ./local_logs/ cloud-storage:healthsync-backups
   ```

2. **Archive Policy:** Configure a Lifecycle Policy to move data to an **Archive/Glacier** tier after 30 days to optimize costs.

---

## Phase 5: Operations & Monitoring

_Related Sessions: [Session 6: Monitoring](../session6_monitoring_and_operations.md)_

### Task 5.1: The Observability Challenge

1. **Centralized Logging:** Describe how you would ship logs from an on-premises Linux server to the Cloud Operations Suite (e.g., using the `Ops Agent`).
2. **Latency Debugging:** Scenario: The doctor's portal is slow.
   - Describe how you would use **Distributed Tracing** to identify if the delay is in the Cloud API, the network Interconnect, or the on-premises Database.
3. **Key Metrics:** List 3 critical metrics you would monitor for the Hybrid Link (e.g., Tunnel State, BGP Flaps, Interconnect Egress Volume).

---

## Final Deliverable: The Hybrid Strategy Proposal

Consolidate your findings into a single proposal for the HealthSync Global executives. Your proposal must include:

- A high-level **Architectural Diagram** showing the Hybrid Hub-and-Spoke networking.
- A **Security Summary** detailing the Zero Trust and PII protection measures.
- A **Migration Roadmap** (Assessment -> Landing Zone -> Migration -> Optimization).
- A **Cost Management Plan** to avoid unexpected egress fees.
