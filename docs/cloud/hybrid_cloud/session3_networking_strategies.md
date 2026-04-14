# Session 3: Networking Strategies

## Objectives

- Understand the methods for connecting on-premises data centers to the public cloud.
- Compare VPNs, Interconnects, and Peerings.
- Learn about secure networking patterns (Gated Ingress/Egress).

## 1. Connectivity Options

To enable a hybrid cloud, you need a "bridge" between environments.

- **VPN (Virtual Private Network):** Secure, encrypted tunnel over the public internet.
  - _Pro:_ Fast to set up, low cost.
  - _Con:_ Performance depends on the internet; not ideal for high-bandwidth data transfers.
- **Dedicated Interconnect (Direct Link):** A physical, private connection between your data center and the cloud provider.
  - _Pro:_ High bandwidth, low latency, consistent performance.
  - _Con:_ Expensive and takes time to install.
- **Partner Interconnect:** Connectivity through a third-party service provider.

## 2. Secure Networking Patterns

- **Mirrored Pattern:** Same networking setup (IP ranges, subnets) in both environments.
- **Meshed Pattern:** All environments (clouds and on-premises) can talk to each other directly.
- **Gated Patterns:** Using a central "hub" (like a Hub-and-Spoke model) to control all traffic entering or leaving the cloud environment.
  - **Gated Ingress:** All incoming traffic goes through a central security appliance.
  - **Gated Egress:** All outgoing traffic is monitored and filtered.

## 3. Best Practices

- Use private IP addressing across the hybrid environment to avoid exposing services to the internet.
- Implement redundant connections to ensure high availability.
- Encrypt data in transit, even when using private lines.

## Practical Exercise: Network Planning

1. You need to migrate 100TB of data from your local server to Azure. Which connectivity option would you choose? Why?
2. Draw a simple "Hub-and-Spoke" network diagram. Show where the VPN/Interconnect sits and where the "gate" (Firewall) is located.
