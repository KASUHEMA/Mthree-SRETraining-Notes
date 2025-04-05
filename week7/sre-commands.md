# 🏦 Banking System Deployment Guide

This guide walks through building, deploying, and monitoring the **BankingSystem** application using Docker, Kubernetes, Prometheus, and Grafana.

---

## 🔧 Prerequisites

- Docker installed and running
- Minikube installed and configured
- kubectl installed
- DockerHub account (for pushing images)
- Kubernetes manifests (`k8s/`, `prometheus/`, `Grafana/` directories)

---

## 🚀 Docker Workflow

### 1. **Login to Docker**

```bash
docker login
```

Logs into DockerHub for pushing/pulling container images.

### 2. **Build Docker Image**

```bash
docker build -t bankingsystem .
```

Builds the Docker image using the Dockerfile in the current directory and tags it as `bankingsystem`.

### 3. **Run Docker Container**

```bash
docker run -d -p 8000:8000 -p 3000:3000 --name banking-system bankingsystem
```

Runs the container in detached mode, maps ports:

- 8000 for Django backend
- 3000 for React frontend

### 4. **If container already exists**

```bash
docker rm -f banking-system
```

Removes the existing container if already running.

### 5. **Check Services**

- Django: [http://localhost:8000](http://localhost:8000)
- Django Metrics: [http://localhost:8000/metrics](http://localhost:8000/metrics)
- React Frontend: [http://localhost:3000](http://localhost:3000)

---

## 📦 DockerHub Deployment

### 6. **Tag and Push Image**

```bash
docker tag <image_name> <your_dockerhub_username>/bankingsystem:v1
docker push <your_dockerhub_username>/bankingsystem:v1
```

Tags the image for DockerHub and pushes it for remote use.

---

## ☈️ Kubernetes Setup

### 7. **Minikube Setup**

```bash
minikube delete
minikube start
```

Resets and restarts the Minikube Kubernetes cluster.

### 8. **Apply Kubernetes Manifests**

```bash
kubectl apply -f k8s/
kubectl get pods
```

Deploys app services (Django, React, Redis, etc.) using Kubernetes manifests.

### 9. **Create Monitoring Namespace**

```bash
kubectl create namespace monitoring
```

Creates a dedicated namespace for monitoring tools (Prometheus, Grafana).

---

## 🔁 Port Forwarding Services

### 10. **Application Services**

```bash
kubectl port-forward svc/django-service 8000:8000
kubectl port-forward svc/react-service 3000:3000
```

Exposes Django and React services locally.

### 11. **Redis Exporter (Metrics)**

```bash
kubectl port-forward svc/redis-exporter 9121:9121
```

Allows Prometheus to scrape Redis metrics locally.

---

## 📊 Prometheus & Grafana Setup

### 12. **Apply Prometheus Config**

```bash
kubectl apply -f prometheus/
kubectl get pods -n monitoring
kubectl port-forward svc/prometheus -n monitoring 9090:9090
```

Deploys Prometheus and opens access on port 9090.
Access at: [http://localhost:9090](http://localhost:9090)

### 13. **Apply Grafana Config**

```bash
kubectl apply -f Grafana/
kubectl get pods -n monitoring
kubectl port-forward svc/grafana -n monitoring 3030:3000
```

Deploys Grafana and makes it available at [http://localhost:3030](http://localhost:3030)

---

## 🧰 Verifications

### 14. **Check Nodes and Services**

```bash
kubectl get nodes -o wide
kubectl get services
```

View node IPs and services. If using NodePort:

- Access via `http://<node-ip>:30008`

---

## 🧾 Conclusion

This guide provides a complete, end-to-end workflow for deploying and monitoring the **BankingSystem** application. By leveraging Docker for containerization, Kubernetes for orchestration, and Prometheus with Grafana for monitoring, teams can ensure scalability, observability, and consistent deployment practices. This setup not only supports robust development but also prepares the system for production-readiness and easy future enhancements.

- All pods should be in `Running` state.
- Django backend accessible at port `8000`
- React frontend running on port `3000`
- Metrics exposed via `/metrics`
- Monitoring stack (Prometheus + Grafana) is live in `monitoring` namespace

