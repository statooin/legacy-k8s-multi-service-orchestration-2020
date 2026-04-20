# Legacy K8s Multi-Service Orchestration (2020)

[⚠️STATUS: ARCHIVAL / HISTORICAL REFERENCE]

## Overview
This project is an architectural milestone from 2020 detailing the manual orchestration of a multi-tier microservices infrastructure on a local Kubernetes cluster. Pre-dating the widespread reliance on managed cloud abstractions (EKS/GKE) and mature GitOps operators, this repository demonstrates a ground-up approach to cluster engineering.

It serves as a public archive of my foundational expertise in cluster networking, persistent volume binding, and interdependent service lifecycle management.

## Infrastructure Stack
The cluster topology is separated into distinct, containerized workloads deployed via declarative YAML manifests.

🌐 **Edge & Networking:**
* **Nginx:** Configured as a reverse proxy with TLS termination.
* **MetalLB:** Simulated L2 load balancing for bare-metal/local ingress.

💾 **State & Persistence:**
* **MySQL:** Dedicated pod with Persistent Volume Claims (PVC) for data durability.
* **FTPS:** Stateful file transfer protocol service.

📊 **Observability:**
* **InfluxDB:** Time-series database for metric aggregation.
* **Grafana:** Visualization layer with pre-provisioned infrastructure dashboards.

## Automation & Provisioning
The deployment pipeline relies on `setup.sh`, an imperative bootstrapping script that handles:
1.  **Cluster Initialization:** Starting Minikube and enabling required hypervisor addons.
2.  **Image Factory:** Programmatic local Docker builds of lightweight, Alpine-based images for every component.
3.  **State Reconciliation:** Applying core manifests, generating OpenSSL secrets for `memberlist`, and exposing the Kubernetes Dashboard.

## 2026 Architectural Context
While imperative shell automation and manual manifest application were standard for local development in 2020, my current enterprise workflows have evolved into highly resilient, automated patterns:

* **Continuous Reconciliation:** Replacing `setup.sh` with ArgoCD/Flux for strict GitOps compliance.
* **Identity & Security:** Moving from static secrets to dynamic, identity-based Zero Trust architectures (SPIFFE/SPIRE).
* **eBPF Observability:** Upgrading from standard metrics servers to high-performance kernel-level observability using Cilium.

---
*This archive is part of my professional evolution, highlighting a deep-dive into the "guts" of Kubernetes orchestration that informs my high-level architectural decisions today.*
