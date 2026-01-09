# Kubernetes Complete Theory 🚀

This repository contains my Kubernetes learning notes including:
- Kubernetes Architecture
- Core Components
- Pods, Deployments, Services
- Networking & Security
- Interview Questions

📌 Created for learning + interview preparation.

## Kubernetes Architecture Diagram

```mermaid
flowchart TB

%% =========================
%% Kubernetes Architecture (Corrected)
%% =========================

subgraph CLUSTER["Kubernetes Cluster"]
  direction TB

  %% ---------- Control Plane ----------
  subgraph CP["Control Plane"]
    direction LR
    API["kube-api-server"]
    ETCD["etcd"]
    SCH["kube-scheduler"]
    KCM["kube-controller-manager"]
    CCM["cloud-controller-manager"]
    CLOUD["Cloud Provider API"]

    API <--> ETCD
    SCH --> API
    KCM --> API
    CCM --> API
    CCM -.-> CLOUD
  end

  %% ---------- Worker Node ----------
  subgraph NODE1["Worker Node"]
    direction TB
    KUBELET["kubelet"]
    KPROXY["kube-proxy"]
    CRI["Container Runtime (containerd/CRI-O)"]

    %% Workloads
    subgraph POD1["Pod (logical)"]
      direction TB
      C1["Container"]
      C2["Container"]
    end

    %% Networking abstraction
    SVC["Service (ClusterIP)"]

    %% Correct relationships
    KUBELET --> CRI
    CRI --> C1
    CRI --> C2

    KPROXY --> SVC
    SVC --> POD1
  end

  %% Node <-> Control Plane communication
  KUBELET <--> API
  KPROXY <--> API
end
