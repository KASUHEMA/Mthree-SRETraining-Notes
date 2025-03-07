# Core of Docker

## 1. The Instructions (Recipe) → Image | Execution → Containers
Think of Docker as a kitchen and Dockerfiles as recipes.
- **Dockerfiles** contain instructions (like a cooking recipe) to build an image.
- **Image** is a ready-to-use package that includes everything needed to run an application (code, dependencies, libraries, etc.).
- **Container** is a running instance of an image (just like cooking a dish from a recipe).

---

## 2. Docker Components
Docker is made up of three main parts:
### a) Docker CLI (Command-Line Interface)
- Used to build and run Docker images and containers.
- Commands like `docker build`, `docker run`, and `docker ps` are executed here.

### b) Docker Daemon
- Background server that manages all Docker operations.
- Takes care of creating, running, and managing containers.

### c) Docker Registry
- A storage system for Docker images.
- You can push (upload) or pull (download) images from a registry.
- **Example:** Docker Hub is a popular registry where developers store and share images.

---

## 3. Essential Docker Commands
### a) Pull an Image
```sh
docker pull <image>
```
- Downloads an image from a registry (e.g., Docker Hub).
- Example: `docker pull python:3.9`

### b) Build an Image
```sh
docker build -t <image-name> .
```
- Creates a Docker image from a Dockerfile.
- Example: `docker build -t my-app .`

### c) Push an Image
```sh
docker push <image>
```
- Uploads an image to a registry.
- Example: `docker push my-app`

### d) Run a Container
```sh
docker run <image>
```
- Starts a container from an image.
- Example: `docker run my-app`

### e) List Running Containers
```sh
docker ps
```
- Shows currently running containers.

---

# Installation of Docker

### Update package list
```sh
sudo apt update
```

### Install prerequisites
```sh
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

### Add Docker's official GPG key
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Add Docker repository
```sh
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

### Update package list again
```sh
sudo apt update
```

### Install Docker
```sh
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### Add user to Docker group
```sh
sudo usermod -aG docker $USER
```

### Verify installation
```sh
docker --version
```

---

![image](https://github.com/user-attachments/assets/44e15e8a-548f-4076-9c21-db87c44e4e24)


![image](https://github.com/user-attachments/assets/c9444259-d3b8-4ab5-8c73-c2baca4beb63)

# Running a Docker Project

### 1. Creating a project directory
```sh
mkdir python-docker-project
cd python-docker-project
```

### 2. Creating subdirectories
```sh
mkdir src tests
```

### 3. Creating necessary files
```sh
touch src/__init__.py src/main.py requirements.txt Dockerfile .dockerignore docker-compose.yml
```

### 4. Project Structure
```
python-docker-project/
├── Dockerfile
├── .dockerignore
├── docker-compose.yml
├── requirements.txt
├── src/
│   ├── __init__.py
│   └── main.py
└── tests/
```

![image](https://github.com/user-attachments/assets/3807fcc9-9423-45e5-b26d-fc92846a76e6)


![image](https://github.com/user-attachments/assets/e176b3a7-4955-4be3-9f97-0a37eead53e3)


![image](https://github.com/user-attachments/assets/180ead7a-d81f-48bd-ba52-e49c6be468da)

---

# Running in VS Code

### Create a virtual environment
```sh
python3 -m venv env
```
### What it does: 
This command creates a virtual environment for our project. A virtual environment is a self-contained directory that contains its own Python binary and can have its own independent set of installed packages, separate from the global Python environment on your system.
### Why use a virtual environment? 
It helps you avoid conflicts between package versions for different projects. For example, one project might need Flask version 2, and another project might need version 1. With a virtual environment, you can manage each project’s dependencies independently.
### How it works:
python3 -m venv: This tells Python to use the venv module to create the virtual environment.
env: This is the name of the directory where the virtual environment will be created. You can name it anything, but "env" or "venv" are common names.

### Activate the virtual environment
```sh
source env/bin/activate
```
### What it does: 
This activates the virtual environment you just created.
### How it works:
**source**: This command is used to execute the activate script in the current shell session.
**env/bin/activate**: This is the path to the activation script inside the env directory you created. When you run this command, it:
  Changes your shell prompt to show you're working inside the virtual environment (it will typically add (env) to your prompt).
  Alters the environment so that Python and pip point to the versions inside the virtual environment, not the system-wide versions.
### Why it’s important: 
Activating the virtual environment makes sure that any Python packages you install with pip (like those listed in requirements.txt) will be installed within the virtual environment, not globally.


### Install dependencies
```sh
pip install -r requirements.txt
```

### Run the Python application
```sh
python3 src/main.py
```

---
![image](https://github.com/user-attachments/assets/90772167-db78-4f80-836a-2f38e0c65291)
### output
![image](https://github.com/user-attachments/assets/0267cc51-79aa-403c-995c-bf47048b3d9b)

![image](https://github.com/user-attachments/assets/1d0b71e3-21a9-4719-b9f4-bf46a2614dff)

# Docker Hub Operations

### 1. Login to Docker
```sh
docker login -u hemakasu
```
![image](https://github.com/user-attachments/assets/44b5ac6e-8172-439c-8e12-660cea26b01c)

### 2. Tag Docker Images
```sh
docker tag python-docker-project-web:latest hemakasu/python-docker-project-web:v1
```

### 3. Push Images to Docker Hub
```sh
docker push hemakasu/python-docker-project-web:v1
```

### 4. Pull Images from Docker Hub
```sh
docker pull hemakasu/python-docker-project-web:v1
```

### 5. Run the Pulled Image
```sh
docker run -d hemakasu/python-docker-project-web:v1
```

### 6. Prune Docker System
```sh
docker system prune
```

---

# Final Summary
1. Logged into Docker Hub.
2. Tagged Docker images.
3. Pushed images to Docker Hub.
4. Added user to Docker group.
5. Cleaned up unused Docker resources.

### Next Steps
- **Pull images**: `docker pull hemakasu/python-docker-project-web:v1`
- **Run containers**: `docker run -d hemakasu/python-docker-project-web:v1`

This guide provides a complete setup and workflow for using Docker effectively. 🚀
for the above code add the matter also u missed it before
