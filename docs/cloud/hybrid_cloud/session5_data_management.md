# Session 5: Data Management and Storage

## Objectives

- Understand data storage options in a hybrid environment.
- Learn about data sovereignty, gravity, and synchronicity.
- Explore hybrid data protection and backup strategies.

## 1. Storage Tiers in Hybrid Cloud

- **Local Storage:** High-performance storage for active workloads on-premises.
- **Cloud Object Storage:** (e.g., Google Cloud Storage, Azure Blob) Scalable, low-cost storage for backups, archives, and web assets.
- **Hybrid Storage Gateways:** Devices (physical or virtual) that sit on-premises and provide a local interface to cloud storage.

## 2. Managing Data Across Environments

- **Data Sovereignty:** Ensuring data is stored and processed within specific geographic or legal boundaries. Hybrid cloud allows keeping sensitive data in-country while using global cloud services for non-sensitive tasks.
- **Data Gravity:** The concept that data is hard to move, so applications should be moved closer to the data.
- **Synchronicity:**
  - **Synchronous Replication:** Data is written to both environments at the same time (High consistency, potential latency).
  - **Asynchronous Replication:** Data is written locally and then copied to the cloud later (Lower latency, potential for data loss in a disaster).

## 3. Data Protection Strategies

- **Hybrid Backup:** Using the cloud as an off-site backup target for on-premises servers.
- **Disaster Recovery (DR):** Maintaining a "pilot light" or "warm standby" environment in the cloud that can take over if the on-premises data center fails.

## Practical Exercise: Data Strategy

1. A hospital needs to store patient records for 50 years. They want to use the cloud to save costs but must keep the "Master" record in their own facility. Design a hybrid storage strategy.
2. Compare "Cloud-to-On-Prem" vs "On-Prem-to-Cloud" data transfer costs (Egress vs Ingress). Which one is usually more expensive?
