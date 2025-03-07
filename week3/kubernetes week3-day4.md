# Project Setup and Deployment Guide

## 1. Setting Up the Project Directory

### Create a Directory for the Python Project
First, create a directory where your Python project will reside and navigate into it:
```bash
mkdir my_python_project
cd my_python_project
```

### Initialize a Git Repository
Initialize a new Git repository to manage version control:
```bash
git init
```

## 2. Project Configuration

### Insert the `pyproject.toml` File
This file defines the dependencies required for the project, including project metadata and package configurations.

### Create the `src` Folder
This folder will contain the main Python files. You can start by adding a simple script, such as:
```python
print("Hello, World!")
```

### Create the `tests` Folder
This directory will hold test cases for unit and integration testing.
```bash
mkdir tests
```

### Create a Dockerfile
A `Dockerfile` is used to create a Docker image for the application. It typically includes instructions for building and running the project inside a container.

### Add a `.gitignore` File
This file helps to ignore unnecessary files like temporary files, logs, and compiled bytecode, improving the project's efficiency.

## 3. Building the Project

### Install the Build Package
The build package is required to create Python distributions:
```bash
pip install build
```

### Build the Wheel File
A wheel file is a standard built-package format for Python:
```bash
python3 -m build --wheel
```
If the above command does not work, use:
```bash
pip install --break-system-packages build
python3 -m build --wheel
```

## 4. Git Configuration and Commit

### Set Up Git User Credentials
Configure Git with your user details:
```bash
git config --global user.email "your_email@gmail.com"
git config --global user.name "your_github_username"
```

### Commit the Changes to GitHub
After making changes, commit them with:
```bash
git commit -m "Initial project setup with Python code and Dockerfile"
```

## 5. Creating the Jenkinsfile

### Create a Jenkinsfile
A `Jenkinsfile` automates the CI/CD pipeline in Jenkins:
```bash
vi Jenkinsfile
```

### Push the Jenkinsfile to GitHub
After creating the `Jenkinsfile`, push it to the GitHub repository:
```bash
git push -u origin main
```

## 6. Setting Up Jenkins Pipeline

### Log Into Jenkins
Open Jenkins in your browser:
```
http://localhost:8080
```
Login using your credentials (default username: `admin`).

### Create a New Item
1. Choose the **Pipeline** option.
2. Name the project and proceed.

### Write the Jenkins Pipeline Script
Initially, test with a basic **Hello World** pipeline:
```groovy
pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello, World!'
            }
        }
    }
}
```
This script helps automate tasks like:
- Cloning the GitHub repository.
- Deleting any outdated files.
- Verifying the repository.
- Building the Python package and Docker image.

### Save and Build
- Click **Save** and then **Build Now** to trigger the pipeline.
- Check the **Console Output** for progress and errors.

## 7. Deploying the Docker Image
The script automates:
- Building the Docker image using the `Dockerfile`.
- Running the image in a container.

### Build the Docker Image
```bash
docker build -t my_python_app .
```

### Run the Container
```bash
docker run -d -p 5000:5000 my_python_app
```

## 8. Troubleshooting

### Common Issues
1. **Wheel File Build Failure**
   - If building fails, set up a virtual environment and retry:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   python3 -m build --wheel
   ```

2. **Git Push Errors**
   - Ensure the repository exists and your credentials are correct.

## 9. Testing the Pipeline
After configuring Jenkins, trigger a new build:
- Click **Build Now**.
- Monitor the **Console Output** to check for errors.

## 10. EC2 Instance Setup

### Connecting to EC2 via SSH
In the later part of the session, you practiced connecting to an AWS EC2 instance running Ubuntu:
```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

This allows remote access to deploy and manage applications on the cloud.

---
This guide provides a step-by-step approach to setting up a Python project, integrating CI/CD using Jenkins, containerizing with Docker, and deploying on an EC2 instance. 🚀

