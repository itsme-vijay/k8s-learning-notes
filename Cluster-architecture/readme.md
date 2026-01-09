Kubernetes is a system that manages applications, runs them on machines, fixes problems automatically, and makes sure everything keeps working.


## What is Kubernetes?

Think of **Kubernetes as a big factory**.

- The factory runs many **applications**
- Applications run inside **containers**
- Kubernetes makes sure:
  - Applications run all the time
  - Broken apps restart
  - Work is shared properly

---

## What is a Cluster?

A **cluster** is the **full factory**.

It has two main parts:

1. **Control Plane** – the factory office (brain)
2. **Worker Nodes** – the factory floor (workers)

👉 Without worker nodes, no work happens.

---

## Worker Nodes (Where work happens)

Worker nodes are **machines that do the real work**.

They:
- Run applications
- Hold **Pods**

### What is a Pod?

A **Pod** is like **one work table**.

- One table can have one or more workers (containers)
- Pods run the application

---

## Control Plane (The Brain)

The control plane is the **factory office**.

It does **not run applications**.  
It only:
- Makes decisions
- Gives orders
- Fixes problems

In big systems, control plane runs on many computers for safety.

---

## Control Plane Components

### kube-apiserver (Front Door)

This is the **main gate**.

- All requests go here first
- Users and components talk through this

Nothing works without kube-apiserver.

---

### etcd (Memory / Notebook)

etcd is like a **big notebook**.

It stores:
- What is running
- What should be running
- Cluster information

📌 Backup is very important.

---

### kube-scheduler (Room Chooser)

This decides:
- Where a new Pod should run
- Which worker node has space

It only **decides**, it does not run Pods.

---

### kube-controller-manager (Problem Fixer)

This is like a **supervisor**.

It checks:
- Is something broken?
- Is anything missing?

If needed:
- It fixes problems automatically

Example:  
If 3 apps are needed and only 2 are running → it starts one more.

---

### cloud-controller-manager (Cloud Helper)

This works **only in cloud** (AWS, Azure, GCP).

It helps with:
- Load balancers
- Cloud machines
- Cloud network

If you use Kubernetes on your laptop → you don’t need this.

---

## Node Components (Inside Worker Node)

### kubelet (Local Manager)

kubelet runs on every worker node.

It:
- Talks to control plane
- Starts containers
- Restarts broken containers

---

### kube-proxy (Traffic Controller)

kube-proxy controls **network traffic**.

It:
- Sends users to the correct Pod
- Balances traffic

Sometimes network tools do this work, so kube-proxy may not be used.

---

### Container Runtime (Engine)

This is the **engine** that runs containers.

Examples:
- containerd
- CRI-O

Kubernetes tells the engine what to run.

---

### Monitoring & Logging

- **Monitoring** → checks CPU and memory
- **Logging** → saves logs in one place

Used to find problems.

---

### Network Plugins (Road System)

These plugins:
- Give IP addresses to Pods
- Connect Pods together

Think of them as **roads inside the factory**.

Examples:
- Calico
- Flannel
- Cilium

---

## Different Kubernetes Setups

### Small Setup
- Control plane and apps on one machine
- Used for learning

### Production Setup
- Control plane on separate machines
- More safe and stable

### Managed Kubernetes
- Cloud company manages control plane
- You only run apps
- Example: EKS, AKS, GKE

---


## Purpose of This Repo

- Learn Kubernetes easily
- Prepare basic understanding
- Beginner friendly
