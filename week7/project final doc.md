# 📓 Banking System - Project Documentation

---

## 🔍 Problem Statement

A modern banking institution needs a robust, secure, and scalable system to manage various banking operations such as customer onboarding, account management, transactions (deposit, withdrawal, transfer), user authentication, and support ticketing. The system must also maintain historical records for auditing and regulatory compliance.

The goal is to design and implement a comprehensive **Banking System** that enables seamless interaction between customers, staff, and banking services, while ensuring data integrity, traceability, and ease of management.

---

## 📈 ER Diagram

The system is modeled with 36 tables in total:
- **20 application tables** for customer, account, transactions, etc.
- **6 Celery-related tables** for background task processing.
- **10 Django internal tables** for admin, auth, sessions, etc.

![Schema 1](https://github.com/user-attachments/assets/9fc32c38-d287-471c-935d-54032c100d9b)

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

This section previously included terminal commands for deploying the application using Docker and Kubernetes. For clarity and simplicity, we are presenting a high-level overview of the deployment steps:

### Deployment Flow Overview

1. **Docker Image Preparation**
   - Login to DockerHub
   - Build and tag the Docker image
   - Push the image to DockerHub repository

2. **Run the Application Locally with Docker**
   - Run the backend (Django) and frontend (React) containers
   - Ensure services are accessible via browser (localhost ports)

3. **Kubernetes Cluster Setup with Minikube**
   - Start/reset Minikube cluster
   - Deploy Kubernetes manifests (YAML files)
   - Expose services and verify pods

4. **Monitoring Stack Installation**
   - Create a dedicated monitoring namespace
   - Deploy Redis Exporter
   - Deploy Prometheus and Grafana
   - Port-forward services for local access

5. **Access Services via Browser**
   - Access NodePort, Prometheus, and Grafana UIs

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

