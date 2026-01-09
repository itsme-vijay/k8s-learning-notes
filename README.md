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
flowchart LR

subgraph Cluster
  subgraph Control_Plane["Control Plane"]
    API[kube-api-server]
    ETCD[etcd]
    CM[kube-controller-manager]
    SCH[kube-scheduler]
    CCM[cloud-controller-manager]
  end

  API <--> ETCD
  CM --> API
  SCH --> API
  CCM --> API

  subgraph Node1["Worker Node 1"]
    K1[kubelet]
    KP1[kube-proxy]
    CR1[Container Runtime]
    P1[Pod]
    P2[Pod]
  end

  K1 --> CR1
  CR1 --> P1
  CR1 --> P2
  KP1 --> P1
end

    Cloud[Cloud Provider API]
    CCM -.-> Cloud
