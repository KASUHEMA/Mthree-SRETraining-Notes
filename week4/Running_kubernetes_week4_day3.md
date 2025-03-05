# Running Kubernetes (Week 4 - Day 3)

## **1. Setting Up Environment**

### Change Directory to Kubernetes Master App:
```bash
cd k8s-master-app/
```

### Add User to Docker Group:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

- `sudo`: Runs the command as an administrator.
- `usermod -aG docker $USER`: Adds the current user to the Docker group.
- `newgrp docker`: Applies the changes immediately.

### Start Minikube with 2200MB Memory:
```bash
sudo minikube start --memory=2200mb --force
```

### Clean Up Docker Resources:
```bash
docker container prune -f
docker image prune -a -f
docker volume prune -f
docker network prune -f
docker system prune -a -f
```

### Check Available Memory:
```bash
free -h
```

---

## **2. Fixing Deployment Issues**

### **1. Update `app.py` to Fix Logging Issue**
```bash
nano ~/k8s-master-app/app/app.py
```
Modify this section:
```python
# Set up logging to print to console and file
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.StreamHandler(),
        logging.FileHandler(os.path.join(os.environ.get('LOG_PATH', '/logs'), 'app.log'))
    ]
)
```
Save with `CTRL + X`, `Y`, `ENTER`.

### **2. Change Directory to App Folder:**
```bash
cd ~/k8s-master-app/app
```

### **3. Rebuild Docker Image:**
```bash
docker build -t k8s-master-app:latest .
```

### **4. Delete Existing Pods:**
```bash
kubectl delete pod -l app=k8s-master -n k8s-demo
```

### **5. Move Back to Project Root:**
```bash
cd ..
```

### **6. Redeploy Application:**
```bash
./scripts/deploy.sh
```

---

## **3. Kubernetes Commands**

### **1. Namespace Management**
```bash
kubectl config view --minify | grep namespace
kubectl apply -f k8s/base/namespace.yaml
kubectl get namespaces
kubectl delete namespace k8s-demo
```

### **2. Deployment Commands**
```bash
kubectl apply -f k8s/base/deployment.yaml
kubectl -n k8s-demo rollout status deployment/k8s-master-app --timeout=180s
kubectl get deployments -n k8s-demo
kubectl describe deployment k8s-master-app -n k8s-demo
kubectl delete -f k8s/base/deployment.yaml
```

### **3. Service Management**
```bash
kubectl apply -f k8s/networking/service.yaml
kubectl get services -n k8s-demo
kubectl describe service k8s-master-app -n k8s-demo
kubectl delete -f k8s/networking/service.yaml
```

### **4. ConfigMaps & Secrets**
```bash
kubectl apply -f k8s/config/configmap.yaml
kubectl get configmaps -n k8s-demo
kubectl apply -f k8s/config/secret.yaml
kubectl get secrets -n k8s-demo
```

### **5. Pod Management**
```bash
kubectl get pods -n k8s-demo
kubectl describe pod <pod-name> -n k8s-demo
kubectl logs -n k8s-demo -l app=k8s-master
kubectl exec -it <pod-name> -n k8s-demo -- /bin/bash
kubectl delete pod <pod-name> -n k8s-demo
```

### **6. Scaling & Auto-Scaling**
```bash
kubectl apply -f k8s/monitoring/hpa.yaml
kubectl get hpa -n k8s-demo
kubectl scale deployment k8s-master-app --replicas=3 -n k8s-demo
```

### **7. Port Forwarding & Exposing Services**
```bash
kubectl -n k8s-demo port-forward svc/k8s-master-app 8080:80
minikube ip
minikube service k8s-master-app -n k8s-demo
```

### **8. Cleaning Up Resources**
```bash
kubectl delete namespace k8s-demo
kubectl delete -f k8s/monitoring/hpa.yaml
kubectl delete -f k8s/networking/service.yaml
kubectl delete -f k8s/base/deployment.yaml
kubectl delete -f k8s/config/secret.yaml
kubectl delete -f k8s/config/configmap.yaml
kubectl delete -f k8s/base/namespace.yaml
docker rmi k8s-master-app:latest
```

---

## **4. Running the Script on AWS EC2**

### **Challenges Faced**
1. **Minikube Not Suitable for AWS EC2**  
   - AWS prefers **EKS (Elastic Kubernetes Service)** over Minikube.
   - Minikube required 2 CPUs but EC2 had limited resources.

2. **Disk Space Limitations**  
   - Default AWS EC2 storage (8GB) was insufficient.
   - Solution:
   ```bash
   sudo growpart /dev/xvda 1
   sudo resize2fs /dev/xvda1
   ```

3. **Cluster Connection Issues**  
   - The script used Minikube’s built-in Kubernetes API (192.168.49.2:8443), which does not work on AWS.
   - Solution:
   ```bash
   aws eks update-kubeconfig --name my-cluster --region us-east-1
   ```

4. **Port Forwarding Issues**  
   - Instead of using `kubectl port-forward`, a **LoadBalancer Service** is needed:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: k8s-master-app
     namespace: k8s-demo
   spec:
     type: LoadBalancer
     selector:
       app: k8s-master
     ports:
       - protocol: TCP
         port: 80
         targetPort: 5000
   ```

---

## **5. Lessons Learned & Next Steps**

### **Lessons Learned**
- **Minikube is not ideal for AWS EC2** – Use **EKS** instead.
- **Disk space issues** can be solved by **expanding AWS EC2 storage**.
- **Kubernetes API issues** arise due to incorrect cluster contexts.
- **LoadBalancer Services** are better than **port-forwarding** in AWS.

### **Next Steps**
- Modify the script to deploy directly to **AWS EKS**.
- Improve storage management to prevent "No Space Left" errors.
- Replace Minikube **NodePort services** with AWS **Load Balancers**.

---

This guide covers running Kubernetes, troubleshooting deployments, and adapting Minikube scripts for AWS EC2. 🚀
