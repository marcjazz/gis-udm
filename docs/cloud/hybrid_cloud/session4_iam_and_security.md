# Session 4: Identity and Access Management (IAM)

## Objectives

- Learn how to manage users and permissions across hybrid environments.
- Understand the role of Directory Services (like Active Directory) in the cloud.
- Explore Single Sign-On (SSO) and Federation.

## 1. Unified Identity

In a hybrid cloud, you don't want separate user accounts for on-premises and the cloud. You need a **Single Source of Truth**.

- **Identity Provider (IdP):** The system that stores and manages digital identities (e.g., Microsoft Entra ID, Google Cloud Identity).
- **Directory Synchronization:** Automatically copying users and groups from an on-premises directory (like LDAP or Active Directory) to the cloud IdP.

## 2. Authentication Patterns

- **Federated Identity:** Users log in using their on-premises credentials. The cloud provider trusts the on-premises IdP to verify the user.
- **Single Sign-On (SSO):** Users log in once and gain access to all systems (on-premises and cloud) without being prompted again.
- **Pass-through Authentication:** The cloud provider passes the credentials back to the on-premises directory for validation.

## 3. Best Practices

- **Principle of Least Privilege:** Grant only the minimum permissions needed for a task.
- **Multi-Factor Authentication (MFA):** Mandatory for all hybrid cloud access to mitigate the risk of compromised credentials.
- **Service Accounts:** Use dedicated, restricted accounts for automated tasks and inter-cloud communication.

## Practical Exercise: Identity Workflow

1. A user joins the company. They are created in the local Active Directory. Describe the steps required for them to access a VM in Google Cloud.
2. What happens if the network connection between the cloud and the on-premises directory is lost? How can you ensure users can still log in?
