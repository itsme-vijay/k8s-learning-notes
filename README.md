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

----------------------------------------------------------
----------------------------------------------------------
```mermaid
flowchart TB
%% =========================
%% CKA-style Kubernetes Architecture
%% =========================

subgraph CL["Kubernetes Cluster"]
  direction TB

  %% ---------- Control Plane ----------
  subgraph CP["Control Plane"]
    direction TB

    subgraph API_LAYER["API Layer"]
      direction LR
      API["kube-api-server"]
      ETCD["etcd"]
      API <--> ETCD
    end

    subgraph CTRL_LAYER["Controllers & Scheduling"]
      direction LR
      SCH["kube-scheduler"]
      KCM["kube-controller-manager"]
      CCM["cloud-controller-manager"]
      SCH --> API
      KCM --> API
      CCM --> API
    end

    subgraph ADDONS_CP["Cluster Add-ons (typically)"]
      direction LR
      DNS["CoreDNS"]
      INGCTL["Ingress Controller (e.g., NGINX)"]
      DNS --> API
      INGCTL --> API
    end

    CLOUD["Cloud Provider API"]
    CCM -.-> CLOUD
  end

  %% ---------- Worker Node ----------
  subgraph N1["Worker Node"]
    direction TB

    subgraph NODE_AGENTS["Node Agents"]
      direction LR
      KUBELET["kubelet"]
      KPROXY["kube-proxy"]
      CNI["CNI Plugin (Calico/Flannel/Cilium)"]
    end

    subgraph RUNTIME["Runtime"]
      direction LR
      CRI["Container Runtime (containerd/CRI-O)"]
      PODS["Pods (one or more containers)"]
      CRI --> PODS
    end

    %% Correct relationships on a node
    KUBELET --> CRI
    CNI --> PODS
    KPROXY --> SVC_RULES["Service Rules (iptables/IPVS)"]
    SVC_RULES --> PODS
  end

  %% ---------- Core Objects / Traffic ----------
  subgraph NET["Traffic & Objects"]
    direction TB
    EXT["Client / Internet"]
    INGRESS["Ingress (resource)"]
    SVC["Service (ClusterIP/NodePort/LB)"]
  end

  %% External traffic flow (typical)
  EXT --> INGCTL
  INGCTL --> INGRESS
  INGRESS --> SVC
  SVC --> SVC_RULES

  %% Control plane <-> node communication
  KUBELET <--> API
  KPROXY <--> API

  %% DNS usage (conceptual)
  PODS -. "DNS queries" .-> DNS
end

