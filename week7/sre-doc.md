# SRE Final Project Documentation

This document outlines the setup and integration of a full monitoring and observability stack using **Docker**, **Kubernetes**, **Prometheus**, and **Grafana**. The stack is used for monitoring a Django + React-based application, along with Redis and Celery integration.

---

## 📦 Project Overview

This project demonstrates Site Reliability Engineering (SRE) practices by integrating:
- **React Frontend** and **Django Backend** in a single Docker image
- **Prometheus** for metrics collection
- **Grafana** for visualization
- **Redis** and **Celery** for asynchronous tasks

---

## ⚙️ Docker
Docker is used to containerize the Django and React application. It ensures that the entire stack (backend, frontend, and monitoring configuration) runs uniformly across different environments.

### Execution Steps:
1. Create a Dockerfile that includes dependencies for both Django and React.
2. Install backend (Python) and frontend (Node.js) libraries.
3. Build the Docker image using the `docker build` command.
4. Run the container using `docker run`, exposing the necessary ports.

This image is then used within Kubernetes for deploying the application.

---

## ☸️ Kubernetes
Kubernetes is used to orchestrate the deployment of Dockerized services across the cluster. It handles scaling, service discovery, and pod management.

### Execution Steps:
1. Define deployment YAMLs for the Django/React app, Prometheus, Grafana, and Redis.
2. Apply the manifests using `kubectl apply -f`.
3. Expose services using NodePort to make them accessible externally.
4. Verify deployment using `kubectl get pods` and `kubectl get services`.

Kubernetes provides a robust platform to run and manage containerized applications reliably.

---

## 📈 Prometheus
Prometheus is used to scrape metrics from services and monitor application performance.

### Execution Steps:
1. Create a ConfigMap with the Prometheus configuration, defining scrape targets.
2. Deploy Prometheus in the `monitoring` namespace.
3. Expose Prometheus using a NodePort service to access it externally.
4. Access the web UI to view targets and metrics.

Prometheus scrapes metrics from Django (via `/metrics`), Redis, and itself to provide real-time insights.

---

## 📊 Grafana
Grafana is used for visualizing metrics collected by Prometheus. It provides dashboards and alerting features.

### Execution Steps:
1. Deploy Grafana with persistent storage in the `monitoring` namespace.
2. Expose Grafana via NodePort to access its UI.
3. Login using default credentials and add Prometheus as a data source.
4. Create or import dashboards to visualize metrics for the app, Redis, and Celery.

Grafana acts as the front-end observability layer in the monitoring stack.

---

## 🎯 SRE Concepts Covered

1. **Observability**: Metrics from Django, Redis, and Prometheus via Prometheus and Grafana dashboards.
2. **Reliability**: Background processing with Celery + Redis, scaling via Kubernetes.
3. **Automation**: YAML definitions and Dockerfile ensure repeatable, scalable deployment.
4. **Monitoring**: Full integration of Prometheus + Grafana, with exporters and service discovery.

---

> This setup offers a robust and production-ready foundation for any app needing real-time monitoring and reliability engineering.

