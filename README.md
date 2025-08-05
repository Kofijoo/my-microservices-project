# My full deployment of Google Cloud's microservices on Kubernetes

This is a full deployment of [Google Cloud's Online Boutique](https://github.com/GoogleCloudPlatform/microservices-demo) — a cloud-native microservices e-commerce application — running locally on Kubernetes with full monitoring, autoscaling, and service observability.

---

## Stack Overview

| Layer        | Tool/Tech                         |
|-------------|-----------------------------------|
| Orchestration | Kubernetes (Minikube)            |
| Services     | 11 Microservices (Go, Python, Java, Node.js, C#) |
| Ingress      | NodePort (Local)                  |
| Storage      | Redis (for cart)                  |
| Monitoring   | Prometheus, Grafana               |
| Autoscaling  | Horizontal Pod Autoscaler (HPA)   |

---

## Microservices Included

- `frontend` – UI layer (Go)
- `cartservice` – Cart state (Redis-backed)
- `checkoutservice` – Order finalization
- `productcatalogservice`, `currencyservice`, `paymentservice`, `emailservice`, `shippingservice`
- `adservice`, `recommendationservice`, `loadgenerator`

---

## Features

- ✅ **Modular Kubernetes Manifests**  
  Split YAMLs for Deployments and Services per microservice

- ✅ **Prometheus Monitoring**  
  Scrapes metrics from all core services. nb

- ✅ **Grafana Dashboards**  
  Preloaded with Pod CPU/Memory dashboards. nb

- ✅ **Horizontal Pod Autoscaling (HPA)**  
  Based on CPU utilization for frontend, cart, and checkout

- ✅ **Health Probes**  
  Readiness & liveness probes for robust deployments

---

## Local Setup

### Prerequisites
- [Minikube](https://minikube.sigs.k8s.io/docs/)
- `kubectl`

### Run the App

```bash
# Start cluster
minikube start

# Apply manifests
kubectl apply -f k8s-manifests/deployments/
kubectl apply -f k8s-manifests/services/
kubectl apply -f k8s-manifests/monitoring/namespace.yaml
kubectl apply -f k8s-manifests/monitoring/ --namespace=monitoring
