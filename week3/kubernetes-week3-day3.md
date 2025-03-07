# Kubernetes

Kubernetes is a powerful open-source platform for automating the deployment, scaling, and management of containerized applications. It allows you to efficiently manage containerized applications in a way that is scalable, resilient, and portable.

## Why Use Kubernetes?
### 1. Container Orchestration:
- Kubernetes helps manage and orchestrate containers, which are lightweight, standalone, executable packages that contain everything needed to run a piece of software (e.g., code, runtime, libraries, and system tools).
- Without Kubernetes, managing large numbers of containers manually can become very complex. Kubernetes automates this by ensuring containers are deployed, scaled, and managed properly.

### 2. Scalability:
- Kubernetes automatically scales your applications up or down based on demand. You can define the number of replicas for a containerized service, and Kubernetes will ensure the desired number of replicas are running.
- Kubernetes can auto-scale, meaning if traffic increases, it can automatically add more containers (pods) to meet demand.

### 3. High Availability and Reliability:
- Kubernetes is designed for high availability and fault tolerance. It automatically restarts or reschedules failed containers across available nodes in a cluster.
- If a container crashes or becomes unresponsive, Kubernetes will detect this and restart it, ensuring minimal downtime.

### 4. Self-Healing:
- Kubernetes provides automatic self-healing features. If a pod (a group of containers) goes down, Kubernetes will replace it automatically. This ensures that your application remains available even in the event of failures.

### 5. Load Balancing and Service Discovery:
- Kubernetes can distribute traffic among different containers to balance the load and improve performance. You can set up services that automatically discover and connect with containers, allowing them to talk to each other.
- It simplifies networking and exposes a single entry point for your application regardless of where the containers are running in the cluster.

### 6. Declarative Configuration:
- With Kubernetes, you define the desired state of your application (e.g., number of replicas, resource limits, networking) in configuration files called "YAML" or "JSON".
- Kubernetes will then ensure that the actual state of the system matches the desired state, and it will correct any discrepancies automatically.

### 7. Portability:
- Kubernetes allows your application to be run on any infrastructure, whether on-premises, in the cloud, or hybrid. It abstracts away the underlying hardware or cloud provider, making your applications portable and easier to manage.

### 8. Ecosystem and Extensibility:
- Kubernetes has a large and growing ecosystem of tools and integrations that extend its capabilities. This includes monitoring, security, networking, logging, and more. Tools like Helm (package manager for Kubernetes) and Prometheus (monitoring) make working with Kubernetes easier.

## Kubernetes Components
### Master Node:
- **API Server**: Exposes the Kubernetes API for communication with cluster components.
- **Scheduler**: Decides which node a newly created pod should run on.
- **Controller Manager**: Ensures the cluster's desired state matches the actual state (e.g., managing replica sets).
- **etcd**: A key-value store for cluster configuration and state data.

### Worker Node:
- **Kubelet**: Ensures containers are running as expected in a pod.
- **Kube Proxy**: Handles network communication, ensuring requests are routed to the correct pods.
- **Container Runtime**: Runs the containers (e.g., Docker, containerd).

### 1. Pods:
- The smallest deployable unit in Kubernetes. A pod can contain one or more containers (usually tightly coupled applications).
- Pods share the same network namespace, meaning they can communicate with each other using localhost.
- Pods are ephemeral, meaning they can be created and destroyed based on need.

### 2. Deployments:
- A higher-level abstraction that manages pods and ensures that a specified number of identical pods are running at all times.
- Deployments provide features like rolling updates and rollbacks to ensure continuous availability of applications.
- They help automate the creation and scaling of pods.

### 3. Services:
- A Kubernetes service defines a policy to access a set of pods. It provides a stable endpoint for accessing pods, regardless of their dynamic nature.
- It can be used for load balancing, distributing traffic to multiple pod instances.
- Types of services include ClusterIP (default, internal access), NodePort (access outside the cluster), and LoadBalancer (cloud provider integration).

## Get Ports in Table Format
```sh
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Ports}}"
```
![image](https://github.com/user-attachments/assets/630e9768-fd1c-404a-92d8-d857ab167d03)

## Installation of Kubernetes
### Running the Shell Script:
```sh
nano install_k8s.sh  # Include the total installation commands in that file
chmod +x install_k8s.sh  # Giving permissions
./install_k8s.sh  # Executing the file
```

# Installation Steps

## Step-by-Step Installation Guide

### Update and Install Required Packages
```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common gnupg2 conntrack
```
- **sudo apt-get update**: Updates the packages that are already installed.
- **sudo apt-get install -y**: Installs multiple packages at a time.

#### Package Descriptions:
1. **apt-transport-https**: Allows secure downloading of software.
2. **ca-certificates**: Ensures that only secure certificates are downloaded.
3. **curl**: A tool to download files from the internet via the command line.
4. **software-properties-common**: Manages additional software sources.
5. **gnupg2**: Provides security for verifying software.
6. **conntrack**: Used for monitoring network connections, including Kubernetes and Docker.

### Remove Existing Docker Installations
```bash
sudo apt-get remove -y docker docker-engine docker.io containerd runc || true
```
Ensures any existing Docker installation is removed or simply moves on if none are found.

### Add Docker Repository and Install Docker
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```
- Adds Docker’s official security key and repository.
- Updates package lists.
- Installs Docker Community Edition and related dependencies.

### Configure Docker
```bash
sudo usermod -aG docker $USER
```
Adds the user to the Docker group.

### Test Docker Installation
```bash
echo "Testing Docker installation..."
sudo docker run hello-world
```
Runs a test container to verify Docker installation.

### Install kubectl
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
rm kubectl
```
- Downloads and installs the latest version of **kubectl**.
- Sets appropriate permissions.
- Removes the original installation file.

### Verify kubectl Installation
```bash
kubectl version --client
```

### Install Minikube
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
rm minikube-linux-amd64
```
- Downloads and installs the latest version of **Minikube**.
- Moves the Minikube binary to make it accessible to all users.
- Deletes the installation file.

### Install Helm
```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```
Downloads and installs Helm (Kubernetes package manager).

### Configure Docker to Start on WSL Startup
```bash
echo "[6/8] Configuring Docker to start on WSL startup..."
echo '# Start Docker daemon automatically when WSL starts
if [ -z "$(ps -ef | grep dockerd | grep -v grep)" ]; then sudo service docker start
fi' >> ~/.bashrc
```
Ensures Docker starts automatically when WSL starts.

### Create Kubernetes Configuration Directory
```bash
mkdir -p ~/.kube
```

### Set Up Kubernetes Command Aliases
```bash
echo 'alias k="kubectl"'
echo 'alias kgp="kubectl get pods"'
echo 'alias kgs="kubectl get services"'
echo 'alias kgd="kubectl get deployments"'
echo 'alias kgn="kubectl get nodes"'
echo 'alias kga="kubectl get all"' >> ~/.bashrc
```
These aliases simplify Kubernetes commands.

### Verify Installed Versions
```bash
minikube version
helm version
kubectl version
docker --version
```
Ensures all installed packages are correctly set up.

### Execute Kubernetes Deployment Scripts
```bash
./simplified-k8s-demo.sh
```
- This script includes requirements, Python files, Docker files, YAML files, deployment files, and Kubernetes configuration.
- After troubleshooting package versions, the following script was executed:
```bash
./flask-fix.sh
```

![image](https://github.com/user-attachments/assets/02e8526d-8cea-4b35-913a-2e4ef1d94526)

This resolves issues related to **requirements and versions**.
---
```sh minikube service flask-app -n mini-demo --url```
   ![image](https://github.com/user-attachments/assets/ec2c47a0-e0f8-4427-9e4c-994593998df1)

![image](https://github.com/user-attachments/assets/49cc4146-e2ba-4ade-a277-35af601f93ef)
Installation and setup are now complete!

## SSH key generartion and pushing the file to git repo
To push code to a repository using SSH key authentication, follow these steps:
### Step 1: Generate SSH Key (if you haven't already)
If you don't have an SSH key yet, you can generate one by running the following command:
```sh ssh-keygen -t rsa -b 4096 -C "kasuhema98@example.com" ```
This will generate a new SSH key pair. You can press Enter to accept the default file location, or specify a custom location.
### Step 2: Add the SSH Key to the SSH Agent
Start the SSH agent and add your SSH private key to it:
```
sheval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```
### Step 3: Add the SSH Key to GitHub (or your Git server)
Copy your SSH public key to your clipboard:
```
sh cat ~/.ssh/id_rsa.pub
https://github.com/settings/keys
```
Then, go to your GitHub (or other Git server) account and add the SSH key to your SSH settings.
### Step 4: Clone the Repository (if you haven't already)
Use SSH to clone your repository:
```sh git clone git@github.com:KASUHEMA/kubernetes.git ```
### Step 5: Push Code to the Repository

### Steps to push the files in to repo: 
```sh
 git init
 git add .
 git remote add origin git@github.com:KASUHEMA/kubernetes.git
 git remote -v
 git remote set-url origin git@github.com:KASUHEMA/kubernetes.git
 git commit -m "Initial commit"
 git branch
 git push -u origin master
```
... 

## Connecting with Jenkins
```sh
sudo usermod -aG docker jenkins
sudo systemctl start jenkins
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Navigate to: [http://localhost:8080/](http://localhost:8080/)

### Jenkins Pipeline Configuration
```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "mini-k8s-demo:latest"
        CONTAINER_NAME = "flask-app"
        K8S_NAMESPACE = "mini-demo"
    }

    stages {
        stage('Clone Repository') {
            steps {
                cleanWs()
                sh 'git clone https://github.com/KASUHEMA/kubernetes.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('kubernetes/app') {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
    }
}
```

### Build and Deploy:
Execute the script:
```sh
./simplified-k8s-demo.sh
```

After troubleshooting, execute:
```sh
./flask-fix.sh
```

Expose the service:
```sh
minikube service flask-app -n mini-demo --url
```

Go to the port: `http://127.0.0.1:34793`

---
This document serves as a comprehensive guide to Kubernetes installation, deployment, and integration with Jenkins.

![image](https://github.com/user-attachments/assets/3447e90c-e75c-4b49-909b-8af75b150712)
