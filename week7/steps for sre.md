# 📓 Banking System - Step-by-Step Deployment

### Step 1: Login to DockerHub
Logs into your DockerHub account to enable pushing and pulling of images.
```bash
docker login
```

### Step 2: Build Docker Image
Creates a Docker image of the BankingSystem application.
```bash
docker build -t bankingsystem .
```

### Step 3: Run Docker Container
Runs the image in a container with exposed ports for backend and frontend.
```bash
docker run -d -p 8000:8000 -p 3000:3000 --name banking-system bankingsystem
```

### Step 4: If Container Already Exists, Remove It
Removes any existing container with the same name to avoid conflicts.
```bash
docker rm -f banking-system
```

### Step 5: Check Service Endpoints
Validates if Django, metrics, and React are accessible.
- Django: http://localhost:8000
- Metrics: http://localhost:8000/metrics
- React: http://localhost:3000

### Step 6: Tag & Push Docker Image
Tags your image and uploads it to DockerHub.
```bash
docker tag <image_name> <your_dockerhub_username>/bankingsystem:v1
docker push <your_dockerhub_username>/bankingsystem:v1
```

### Step 7: Reset & Start Minikube
Starts a clean Kubernetes cluster using Minikube.
```bash
minikube delete
minikube start
```

### Step 8: Deploy Kubernetes Resources
Applies Kubernetes YAML files and checks pod status.
```bash
kubectl apply -f k8s/
kubectl get pods
```

### Step 9: Create Monitoring Namespace
Sets up a dedicated namespace for Prometheus and Grafana.
```bash
kubectl create namespace monitoring
```

### Step 10: Port-Forward Django and React Services
Allows local access to Django and React running inside the cluster.
```bash
kubectl port-forward svc/django-service 8000:8000
kubectl port-forward svc/react-service 3000:3000
```

### Step 11: Port-Forward Redis Exporter
Exposes Redis metrics for Prometheus to scrape.
```bash
kubectl port-forward svc/redis-exporter 9121:9121
```

### Step 12: Deploy Prometheus
Deploys Prometheus and makes it accessible on localhost.
```bash
kubectl apply -f prometheus/
kubectl get pods -n monitoring
kubectl port-forward svc/prometheus -n monitoring 9090:9090
```

### Step 13: Deploy Grafana
Deploys Grafana for visualizing metrics data.
```bash
kubectl apply -f Grafana/
kubectl get pods -n monitoring
kubectl port-forward svc/grafana -n monitoring 3030:3000
```

### Step 14: Get Node Info and Service Details
Lists all Kubernetes nodes and services.
```bash
kubectl get nodes -o wide
kubectl get services
```

### Step 15: Access the Application
Access your app and monitoring tools via browser.
- NodePort example: `http://<node-ip>:30008`
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3030`

---

## ✅ Conclusion
This step-by-step guide simplifies the deployment and monitoring of the **BankingSystem** application. It ensures a smooth developer workflow by combining Docker for packaging, Kubernetes for orchestration, and Prometheus + Grafana for observability. Follow these steps to get your system up and running efficiently.

