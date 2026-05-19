# 📑 Lab Assignment: Zero-Trust Hybrid Observability & Architecture Reconstruction

> **Course Module:** Advanced Hybrid Cloud Systems & Infrastructure Engineering
> **Deadline:** Prior to next session kick-off
> **Estimated Time Commitment:** 2–3 Hours
> **Submission Requirement:** Markdown or Notion Link showing screenshots of your working NetBird Peer Map, passing curl commands, and active Grafana panels.

---

## 🎯 1. Lab Objectives & Architectural Vision

In this assignment, you are tasked with reconstructing and validating the decoupled, zero-trust monitoring architecture implemented during today's live lecture.

The goal is to securely bridge a localized, private container runtime environment to an out-of-band analytics engine without exposing corporate infrastructure or metrics pipelines to the public internet ($0.0.0.0/0$).

### 🏗️ Core Structural Diagram

```
  [ Local Host / Laptop ]                 [ Private Infrastructure Node ]
  ┌───────────────────────┐               ┌───────────────────────────────────┐
  │ Docker Engine         │               │ K3s Cluster Engine (Kubernetes)   │
  │  └─► Grafana Container│               │  └─► Pod: prometheus-core         │
  │        (Port 3000)    │               │        (Listening on port 9090)   │
  └───────────┬───────────┘               └─────────────────┬─────────────────┘
              │                                             │
              ▼                                             ▼
       (NetBird Interface)                           (NetBird Interface)
       [Overlay IP: 100.X.X.A] ◄═════ encrypted ════► [Overlay IP: 100.X.X.B]
                                    WireGuard Tunnel

```

---

## 🛠️ 2. Core Components Required

Before beginning execution, verify that your local environment satisfies the following checklist:

| Component                 | Minimum Specification / Tooling                         | Deployment Scope                                |
| ------------------------- | ------------------------------------------------------- | ----------------------------------------------- |
| **Local Hypervisor / VM** | Ubuntu Server 22.04 LTS (or equivalent Linux distro)    | Host environment for the cluster                |
| **K8s Distribution**      | **K3s** (Lightweight Kubernetes by Rancher)             | Runs internal applications & metrics collection |
| **Mesh Networking Agent** | **NetBird Agent** (Free Account Tier)                   | Manages point-to-point overlay paths            |
| **Orchestration Tool**    | **Helm v3** installed on your control path              | Packages the observability architecture         |
| **Local Visualizer**      | **Docker Desktop** or native Docker daemon on your host | Runs isolated Grafana instances                 |

---

## 📝 3. Step-by-Step Implementation Procedure

### 🔓 Step 3.1: Establishing the Secure Mesh Overlay

1. Register for a free account at [NetBird.io](https://netbird.io/).
2. Install the NetBird system daemon onto your primary workstation/laptop and your destination Linux VM using the automated runtime package manager:

```bash
curl -fsSL https://pkgs.netbird.io/install.sh | sh

```

3. Initialize the daemon on both environments to link them into your secure account tenant pool:

```bash
sudo netbird up

```

4. Navigate to your administrative NetBird Dashboard Panel, locate both registered peers, and copy the assigned virtual overlay IPs (which follow the structural format: `100.xxx.xxx.xxx`).

---

### 📦 Step 3.2: Spinning up the K3s Runtime Cluster

If you do not have a working cluster on your destination VM, instantiate a clean, lightweight instance running without standard cloud provider ingress controllers:

```bash
curl -sfL https://get.k3s.io | sh -

```

Verify your environment context is online and responsive:

```bash
sudo kubectl get nodes -o wide

```

---

### 📊 Step 3.3: Injecting the Core Metrics Engine via Helm

1. Register the unified monitoring repository charts within your local Helm binary configuration:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

```

2. Deploy the standard monitoring stack into its own dedicated cluster namespace context:

```bash
helm install monitoring prometheus-community/kube-prometheus-stack \
  --create-namespace --namespace monitoring

```

3. Monitor your environment execution state. Wait until all underlying system operator systems show a `Running` or `Completed` state before moving forward:

```bash
kubectl get pods -n monitoring

```

---

### ⚙️ Step 3.4: Bypassing the Host-Header 404 Route Block

> **Architectural Core Concept:** The Prometheus binary inside the Helm chart enforces a safety rule: `--web.external-url=http://monitoring-kube-prometheus-prometheus.monitoring:9090`. If external traffic queries the engine using a direct IP rather than this exact DNS address string, the application layer throws a `404 Not Found` error.

To circumvent this for our out-of-band dashboard, we must tunnel straight past the service route filters into the target pod directly.

1. Locate the exact alphanumeric pod title assigned to your instance engine runtimes:

```bash
kubectl get pods -n monitoring -l app.kubernetes.io/name=prometheus

```

2. Kill any old, dead, or hanging background cluster proxy forwarding channels:

```bash
pkill kubectl -9

```

3. Run an active out-of-band proxy channel bound explicitly to all local network listeners (`0.0.0.0`), matching your precise pod name destination:

```bash
sudo kubectl port-forward --address 0.0.0.0 pod/<YOUR_SPECIFIC_PROMETHEUS_POD_NAME_HERE> -n monitoring 9090:9090 &

```

---

### 🧪 Step 3.5: Network Route Verification

From your **primary workstation/laptop terminal**, check that your connection can cross the virtual WireGuard tunnel into the cluster:

```bash
# Execute a standard non-header GET query
curl http://<YOUR_CLUSTER_VM_NETBIRD_IP>:9090/graph

```

- **Success Criteria:** The terminal returns a large body of raw HTML code structure.
- _Note:_ If you use a `curl -I` request, Prometheus will drop it with a `405 Method Not Allowed` because it explicitly mandates standard `GET` requests.

---

### 📈 Step 3.6: Connecting Your Local Grafana Engine

1. Launch an isolated, clean instance of Grafana using your host machine's native Docker environment:

```bash
docker run -d -p 3000:3000 --name=hybrid-grafana grafana/grafana-oss

```

2. Navigate your web browser to `http://localhost:3000` (Default credentials: Admin/Admin) and configure a new **Prometheus Data Source**.
3. **Crucial Connection Fields:**

- **URL:** Set this to your target cluster's NetBird IP address: `http://100.xxx.xxx.xxx:9090`
- **HTTP Method:** Explicitly change this drop-down option from `POST` to `GET`.

4. Click **Save & Test**. The connection banner will turn green.

---

## 🚀 4. The Engineering Extension Challenge (Preparation for Next Session)

To achieve maximum grading points, you must prepare your environment infrastructure for our upcoming enterprise governance class.

### 🔐 Part A: Spin Up an Identity Provider (IdP)

Deploy a centralized credential store directly inside your environment framework. You can run native OpenLDAP, or spinning up a containerized **Keycloak** identity wrapper is highly recommended:

```bash
docker run -d -p 8080:8080 --name=local-idp \
  -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin \
  quay.io/keycloak/keycloak:latest start-dev

```

### 📋 Part B: Architectural Formulation Task

Write a high-level technical paragraph or provide a layout block in your submission detailing how you plan to orchestrate **Identity Federation** across this layout once we return. Your answer must explain:

1. How a local directory user can authenticate against Google Cloud IAM platforms without managing duplicate credentials.
2. The specific purpose of **Google Cloud Directory Sync (GCDS)** in managing secure user directory transfers across hybrid clouds.
