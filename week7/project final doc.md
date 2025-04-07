# 📓 Banking System - Project Documentation

---

## 🔍 Problem Statement

A modern banking institution needs a robust, secure, and scalable system to manage various banking operations such as customer onboarding, account management, transactions (deposit, withdrawal, transfer), user authentication, and support ticketing. The system must also maintain historical records for auditing and regulatory compliance.

The goal is to design and implement a comprehensive **Banking System** that enables seamless interaction between customers, staff, and banking services, while ensuring data integrity, traceability, and ease of management.

---

## 📊 ER Diagram

The system is modeled with 36 tables in total:
- **20 application tables** for customer, account, transactions, etc.
- **6 Celery-related tables** for background task processing.
- **10 Django internal tables** for admin, auth, sessions, etc.

![Schema 1](https://github.com/user-attachments/assets/ed28df99-fad8-45ba-861c-11f808df8655)

---

## ⚙️ Functionalities

### 1. **Customer Management**
- Register new customers with personal details.
- Store and manage customer addresses.
- Link users with customer accounts.

### 2. **User Management**
- User login and logout functionalities.
- Role-based access control (e.g., staff or non-staff).
- Maintain login/logout logs.

### 3. **Account Management**
- Create new accounts linked to a customer.
- Maintain different account types (savings, checking, etc.).
- Enable account editing and updates.
- Store deleted account information for auditing.

### 4. **Branch Management**
- Manage branch details including name and location.
- Link accounts to specific branches.

### 5. **Transaction Management**
- Record all types of transactions (deposits, withdrawals, transfers).
- Maintain logs with timestamps for each transaction.
- Track balances for each account.

### 6. **Deposit & Withdrawals**
- Allow deposits to an account.
- Allow withdrawals from an account.
- Each operation links to a transaction ID for traceability.

### 7. **Funds Transfer**
- Transfer funds from one account to another (transferout & transferin).
- Store details like sender/receiver account numbers, amount, and timestamp.

### 8. **Support Ticket System**
- Allow users to raise tickets for issues.
- Admin/staff can update and resolve tickets.
- Maintain ticket status and resolution messages.

### 9. **Interest Table Management**
- Store and manage interest rates for different account types.
- Update rates as required.

### 10. **Announcements**
- Post announcements for users/customers (e.g., system updates, new features).
- Include title, message, creation, and update timestamps.

### 11. **Audit Logs and History**
- Maintain logs for deleted accounts.
- Track login/logout events.
- Store past balances and account edits.

---

## 🚀 Step-by-Step Deployment Guide

### Step 1: Login to DockerHub
```bash
docker login
```

### Step 2: Build Docker Image
```bash
docker build -t bankingsystem .
```

### Step 3: Run Docker Container
```bash
docker run -d -p 8000:8000 -p 3000:3000 --name banking-system bankingsystem
```

### Step 4: If Container Already Exists, Remove It
```bash
docker rm -f banking-system
```

### Step 5: Check Service Endpoints
- Django: http://localhost:8000
- Metrics: http://localhost:8000/metrics
- React: http://localhost:3000

### Step 6: Tag & Push Docker Image
```bash
docker tag <image_name> <your_dockerhub_username>/bankingsystem:v1
docker push <your_dockerhub_username>/bankingsystem:v1
```

### Step 7: Reset & Start Minikube
```bash
minikube delete
minikube start
```

### Step 8: Deploy Kubernetes Resources
```bash
kubectl apply -f k8s/
kubectl get pods
```

### Step 9: Create Monitoring Namespace
```bash
kubectl create namespace monitoring
```

### Step 10: Port-Forward Django and React Services
```bash
kubectl port-forward svc/django-service 8000:8000
kubectl port-forward svc/react-service 3000:3000
```

### Step 11: Port-Forward Redis Exporter
```bash
kubectl port-forward svc/redis-exporter 9121:9121
```

### Step 12: Deploy Prometheus
```bash
kubectl apply -f prometheus/
kubectl get pods -n monitoring
kubectl port-forward svc/prometheus -n monitoring 9090:9090
```

### Step 13: Deploy Grafana
```bash
kubectl apply -f Grafana/
kubectl get pods -n monitoring
kubectl port-forward svc/grafana -n monitoring 3030:3000
```

### Step 14: Get Node Info and Service Details
```bash
kubectl get nodes -o wide
kubectl get services
```

### Step 15: Access the Application
- NodePort example: `http://<node-ip>:30008`
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3030`

---

## 🔧 Site Reliability Engineering (SRE) Tools Used
- **Docker**: Containerization of app components.
- **Kubernetes**: Cluster orchestration for scaling and reliability.
- **Jenkins**: CI/CD automation.
- **Prometheus**: Metrics collection.
- **Grafana**: Dashboard visualization of metrics.

---

## ✅ Conclusion
This comprehensive Banking System enables secure, scalable financial operations and includes monitoring capabilities for high reliability. The architecture supports modern DevOps and SRE practices, ensuring production-readiness and observability.

*Next: Add Kubernetes architecture diagram once the image is shared.*

