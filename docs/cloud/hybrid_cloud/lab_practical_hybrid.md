# Practical Lab: Hybrid Cloud Scenarios

This lab guide provides step-by-step instructions for implementing four key hybrid cloud scenarios. These exercises are designed to give you hands-on experience with networking, application deployment, disaster recovery, and multi-cloud Kubernetes.

---

## Scenario 1: Networking - The Universal Overlay Network
**Goal:** Create a secure, encrypted overlay network (Mesh VPN) that connects resources across Local, Linode, and GCP using Tailscale or Wireguard.

### Step 1: Install Tailscale on All Nodes
1. **Local Machine:** Download and install Tailscale from [tailscale.com](https://tailscale.com/download).
2. **Linode VPS:**
    ```bash
    curl -fsSL https://tailscale.com/install.sh | sh
    sudo tailscale up
    ```
3. **GCP Instance:**
    ```bash
    curl -fsSL https://tailscale.com/install.sh | sh
    sudo tailscale up
    ```

### Step 2: Authenticate and Verify
1. Follow the authentication links provided in the terminal for each node.
2. Once authenticated, verify connectivity from your local machine:
    ```bash
    tailscale status
    ping <linode-tailscale-ip>
    ping <gcp-tailscale-ip>
    ```

### Step 3: Enable Subnet Routing (Optional)
If you want to access the entire VPC/Local network behind a node:
1. On the node: `sudo tailscale up --advertise-routes=10.0.0.0/24` (replace with your subnet).
2. In the Tailscale Admin Console, enable the "Subnet Route" for that device.

---

## Scenario 2: Application Deployment - Distributed Tiered Architecture
**Goal:** Deploy a 3-tier application where components are distributed across different environments.
- **Database:** PostgreSQL (Local)
- **App Server:** Flask/Node.js (Linode)
- **Object Storage:** Cloud Storage (GCP)

### Step 1: Set up Local Database
1. Install and start PostgreSQL.
2. Create a database and a user that allows connections from the Tailscale IP of the Linode server.
3. Update `pg_hba.conf` and `postgresql.conf` to allow remote connections on the Tailscale interface.

### Step 2: Set up GCP Cloud Storage
1. Create a Bucket in GCP.
2. Create a Service Account with `Storage Object Admin` permissions.
3. Download the JSON key file.

### Step 3: Deploy Application on Linode
1. Clone your application code.
2. Configure the application to use:
    - The Local Machine's Tailscale IP for the database connection.
    - The GCP Service Account key for storage operations.
3. Start the application and verify it can read/write to both the local DB and GCP storage.

---

## Scenario 3: Disaster Recovery & Backup - Tiered 3-2-1 Strategy
**Goal:** Implement a robust backup strategy where data flows from Local to Linode to GCP.
- **Local:** Primary Data
- **Linode:** Hot/Warm Backup (S3-compatible Object Storage)
- **GCP:** Archive (Cloud Storage Archive Class)

### Step 1: Local to Linode (Hot Backup)
1. Use `rclone` to sync local data to Linode Object Storage.
    ```bash
    rclone sync /path/to/local/data linode-s3:my-backup-bucket
    ```

### Step 2: Linode to GCP (Archive)
1. Use `rclone` or a scheduled script to move older backups from Linode to GCP Archive.
    ```bash
    rclone copy linode-s3:my-backup-bucket gcp-storage:my-archive-bucket --storage-class ARCHIVE
    ```

### Step 3: Verify Restoration
1. Delete a local file.
2. Restore it from the Linode backup.
3. Simulate a total Linode failure and restore from the GCP archive.

---

## Scenario 4: Multi-cloud Kubernetes - The Spanning K3s Cluster
**Goal:** Create a single Kubernetes cluster with nodes in different clouds.
- **Master Node:** Linode
- **Worker Node 1:** Local Machine
- **Worker Node 2:** GCP Instance

### Step 1: Initialize K3s Master (Linode)
1. Install K3s with the Tailscale IP as the advertise address:
    ```bash
    curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--node-ip=<linode-tailscale-ip> --flannel-iface=tailscale0" sh -
    ```
2. Retrieve the node token: `sudo cat /var/lib/rancher/k3s/server/node-token`

### Step 2: Join Worker Nodes (Local & GCP)
1. Install K3s agent on workers, pointing to the Linode master:
    ```bash
    curl -sfL https://get.k3s.io | K3S_URL=https://<linode-tailscale-ip>:6443 \
    K3S_TOKEN=<node-token> INSTALL_K3S_EXEC="--node-ip=<worker-tailscale-ip> --flannel-iface=tailscale0" sh -
    ```

### Step 3: Verify Cluster Status
1. On the Master node:
    ```bash
    kubectl get nodes -o wide
    ```
2. You should see all three nodes (Linode, Local, GCP) in a `Ready` state, communicating over the overlay network.
