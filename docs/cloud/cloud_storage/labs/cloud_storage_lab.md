# Lab: Cloud Storage Exploration and Engineering

## Introduction

This lab is designed to move beyond theoretical definitions. You will research, compare, and implement cloud storage solutions. Instead of following a tutorial, you are expected to consult official documentation, analyze trade-offs, and justify your architectural decisions.

---

## 1. The Storage Matrix: Research & Comparison

Cloud storage is not a "one size fits all" solution. Your first task is to research the three fundamental types of storage and build a comprehensive comparison matrix.

### Task 1.1: Deep Dive Research

Research **Block Storage**, **File Storage**, and **Object Storage**. Focus on how they handle data at the physical and logical layers.

### Task 1.2: Build the Comparison Matrix

Fill in the following table based on your research. Do not copy-paste definitions; use technical criteria.

| Feature               | Block Storage         | File Storage | Object Storage |
| :-------------------- | :-------------------- | :----------- | :------------- |
| **Data Unit**         | e.g. 512-byte sectors |              |                |
| **Common Protocols**  |                       |              |                |
| **Scaling Mechanism** |                       |              |                |
| **Metadata Support**  |                       |              |                |
| **Typical Latency**   |                       |              |                |
| **Consistency Model** |                       |              |                |
| **Cost Efficiency**   |                       |              |                |

### Task 1.3: Provider Mapping

Identify the equivalent service for each storage type across the "Big Three" cloud providers (AWS, Azure, GCP).

---

## 2. Security Engineering: IAM Policy Construction

Providing "Full Access" is a security failure. You must implement the principle of least privilege.

### Scenario

You are a Cloud Engineer tasked with securing an S3-compatible bucket named `finance-records-2024`.

### Challenge

Write a JSON IAM policy that meets the following requirements:

1. Allow a specific user to **list** the contents of the bucket.
2. Allow the user to **read (download)** objects from the bucket.
3. **Explicitly Deny** the ability to delete any object, even if they have other permissions.
4. The policy must only apply to the `finance-records-2024` bucket.

> **Resource for Research**: [AWS IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html)

---

## 3. Practical Implementation: Minio CLI & Object Management

While the GUI is useful for beginners, professionals use the Command Line Interface (CLI) for automation and efficiency.

### Step 1: Initialize the Environment

Launch a local S3-compatible environment using Docker:

```bash
docker run -d -p 9000:9000 -p 9001:9001 \
  --name minio-lab \
  -e "MINIO_ROOT_USER=admin" \
  -e "MINIO_ROOT_PASSWORD=password123" \
  quay.io/minio/minio server /data --console-address ":9001"
```

### Step 2: The `mc` (Minio Client) Challenge

Install the Minio Client (`mc`) on your local machine. Use the [Minio CLI Documentation](https://min.io/docs/minio/linux/reference/minio-cli.html) to complete the following:

1. **Configure Alias**: Create an alias for your local server.
2. **Bucket Lifecycle**: Create a bucket named `sensitive-data`.
3. **Quota Management**: Research and apply a **hard quota** of 100MB to the `sensitive-data` bucket.
4. **Anonymous Access**: Research how to set the policy of a bucket to `download` (public read-only) using only the CLI.
5. **Versioning**: Enable versioning on your bucket and demonstrate how to recover a "deleted" file.

---

## 4. Architectural Decision Records (ADR)

You are presented with the following business scenarios. For each, write a short (1-2 paragraph) proposal.

**Your proposal must justify:**

- Choice of Storage Type (Block, File, Object, or Ephemeral).
- Choice of Cloud Provider Service.
- Impact on Cost vs. Performance (IOPS/Bandwidth).
- Security considerations (Encryption at rest/in transit).

### Scenario A: Media Streaming Startup

A new platform needs to store and serve 500TB of video content to global users. The data is rarely modified once uploaded but frequently accessed.

### Scenario B: High-Frequency Trading (HFT) App

An application requires the lowest possible latency for processing transient data. The data is lost if the instance restarts, which is acceptable for this specific workload.

### Scenario C: Enterprise ERP Migration

A legacy ERP system requires a shared filesystem that multiple Linux instances can mount simultaneously via NFS to share configuration and state files.

### Scenario D: State-of-the-art PostgreSQL Cluster

A database requires consistent sub-millisecond latency and the ability to take point-in-time snapshots for disaster recovery.

---

## 5. Self-Assessment & Research Questions

Before finishing, research and answer the following:

1. What is the "Thundering Herd" problem in shared file storage?
2. Why is "Eventual Consistency" a challenge for distributed object storage, and how have modern providers (like S3) recently changed their consistency model?
3. Compare **Cold Archive** storage (e.g., Glacier) vs. **Standard** storage in terms of retrieval time and "egress" costs.
