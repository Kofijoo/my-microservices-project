# Monitoring Setup for Microservices Demo

This directory contains Kubernetes manifests for setting up monitoring with Prometheus and Grafana.

## Components

- **Prometheus**: Collects metrics from services
- **Grafana**: Visualizes metrics in dashboards
- **HPAs (Horizontal Pod Autoscalers)**: Automatically scales services based on CPU usage

## Deployment

Apply the manifests in the following order:

```bash
# Create namespace
kubectl apply -f namespace.yaml

# Deploy Prometheus
kubectl apply -f prometheus-configmap.yaml
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f prometheus-service.yaml

# Deploy Grafana
kubectl apply -f grafana-datasource-config.yaml
kubectl apply -f grafana-dashboard-config.yaml
kubectl apply -f grafana-deployment.yaml
kubectl apply -f grafana-service.yaml

# Apply HPAs
kubectl apply -f frontend-hpa.yaml
kubectl apply -f cartservice-hpa.yaml
kubectl apply -f checkoutservice-hpa.yaml
```

## Accessing Dashboards

- **Prometheus**: Access via `http://<node-ip>:30090` (if NodePort is configured)
- **Grafana**: Access via `http://<node-ip>:30003`
  - Default credentials: admin/admin

## Dashboards

The default dashboard shows:
- CPU usage by pod
- Memory usage by pod

## Autoscaling

The following services are configured to autoscale:
- frontend: 1-5 replicas based on 70% CPU utilization
- cartservice: 1-5 replicas based on 70% CPU utilization
- checkoutservice: 1-5 replicas based on 70% CPU utilization