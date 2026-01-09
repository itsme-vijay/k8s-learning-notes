# Kubernetes Complete Theory 🚀

This repository contains my Kubernetes learning notes including:
- Kubernetes Architecture
- Core Components
- Pods, Deployments, Services
- Networking & Security
- Interview Questions

📌 Created for learning + interview preparation.

flowchart LR
    subgraph Cluster
        subgraph Control_Plane["Control Plane"]
            API[kube-api-server]
            ETCD[etcd]
            CM[kube-controller-manager]
            SCH[kube-scheduler]
            CCM[cloud-controller-manager]

            API <---> ETCD
            CM --> API
            SCH --> API
            CCM --> API
        end

        subgraph Node1["Worker Node 1"]
            K1[kubelet]
            KP1[kube-proxy]
            CR1[Container Runtime]
            P1[Pod]
            P2[Pod]

            K1 --> CR1
            CR1 --> P1
            CR1 --> P2
            KP1 --> P1
        end

        subgraph Node2["Worker Node 2"]
            K2[kubelet]
            KP2[kube-proxy]
            CR2[Container Runtime]
            P3[Pod]

            K2 --> CR2
            CR2 --> P3
            KP2 --> P3
        end

        API --> K1
        API --> K2
    end

    Cloud[Cloud Provider API]
    CCM -.-> Cloud
