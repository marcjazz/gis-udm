# Session 7: Security and Compliance Deep Dive

## Objectives

- Understand the "Shared Responsibility Model" in a hybrid context.
- Identify hybrid-specific security risks and how to mitigate them.
- Learn about Zero Trust architecture and its application to hybrid cloud.

## 1. Shared Responsibility Model

Security is a partnership between you and the cloud provider.

- **Cloud Provider Responsibility:** Security **OF** the cloud (Physical data centers, core networking, hardware).
- **Customer Responsibility:** Security **IN** the cloud (Your data, application code, identity management, and the "bridge" connecting to on-premises).

## 2. Hybrid Security Risks

- **Increased Attack Surface:** More entry points (on-premises, cloud, and the connection between them).
- **Misconfigurations:** Inconsistent security policies between environments.
- **Access Control:** Complications in managing permissions across different systems.
- **Insecure Connections:** Risk of data interception if tunnels are not properly encrypted.

## 3. Mitigating Risks

- **Zero Trust Architecture:** Never trust, always verify. Every request (even from within the network) must be authenticated and authorized.
- **Encryption Everywhere:** Use encryption for data at rest (on-premises and in the cloud) and data in transit.
- **Regular Audits:** Use automated tools (e.g., Security Command Center) to scan for vulnerabilities and compliance violations.

## Practical Exercise: Security Audit

1. A user is able to access a database in the cloud from an unmanaged personal laptop at home. Which security principle has been violated?
2. List 3 security measures you would implement to protect the connection between your data center and the cloud.
3. Define the "Shared Responsibility" for a Managed Kubernetes service (like GKE or AKS) in a hybrid setup.
