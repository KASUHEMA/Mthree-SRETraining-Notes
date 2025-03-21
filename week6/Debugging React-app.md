## Changes to `complete-react-sre-script.sh`

### Change 1
- **Original Line:**
  ```bash
  if ! grep -q Microsoft /proc/version; then
  ```
- **Updated Line:**
  ```bash
  if ! grep -qEi "(microsoft|wsl)" /proc/version; then
  ```
- **Line Number:** 82 (approximate, verify in the actual file)

**Description:** This change expands the check for WSL by making it case-insensitive and including variations like "wsl" explicitly.

---

## Changes to `deploy_app.py`

### Change 2
- **Original Function:** `create_namespaces`
  ```python
  def create_namespaces():
      """Create necessary Kubernetes namespaces."""
      log("INFO", "Creating Kubernetes namespaces...")
  
      namespaces = ["react-sre-app", "monitoring"]
      for namespace in namespaces:
          result = run_command([
              KUBECTL_CMD, "create", "namespace", namespace, "--dry-run=client", "-o", "yaml"
          ], timeout=10)
  
          if result is None:
              log("ERROR", f"Failed to generate namespace YAML for {namespace}")
              return False
  
          apply_result = run_command(f"{KUBECTL_CMD} apply -f -", timeout=10, shell=True, retry=3)
  
          if apply_result is None:
              log("ERROR", f"Failed to create namespace {namespace}")
              return False
  
      log("INFO", "Kubernetes namespaces created successfully")
      return True
  ```
- **Updated Function:**
  ```python
  def create_namespaces():
      """Ensure necessary Kubernetes namespaces exist."""
      log("INFO", "Ensuring required Kubernetes namespaces exist...")
  
      namespaces = ["react-sre-app", "monitoring"]
      for namespace in namespaces:
          if namespace_exists(namespace):
              log("INFO", f"Namespace '{namespace}' already exists. Skipping creation.")
              continue
  
          log("INFO", f"Creating namespace: {namespace}")
  
          create_result = run_command(
              [KUBECTL_CMD, "create", "namespace", namespace],
              timeout=10,
              retry=3
          )
  
          if create_result is None:
              log("ERROR", f"Failed to create namespace '{namespace}'")
              return False
  
      log("INFO", "All required namespaces are ready.")
      return True
  ```
- **Line Number:** 285 (approximate, verify in the actual file)

### Change 3
- **New Function:** `namespace_exists`
  ```python
  def namespace_exists(namespace):
      """Check if a Kubernetes namespace already exists."""
      result = run_command(
          [KUBECTL_CMD, "get", "namespace", namespace, "-o", "jsonpath={.metadata.name}"],
          timeout=10
      )
      return result is not None and namespace in result
  ```
- **Line Number:** 275 (approximate, verify in the actual file)

**Description:** Added a function `namespace_exists` to check if a namespace exists before attempting creation, improving efficiency and avoiding redundant operations.

### Change 4
- **Updated Function:** `run_command`
  - **Added Parameter:** `cwd=None`
  - **Updated `subprocess.run` Calls:** Included `cwd=cwd` to allow specifying the working directory.
  - **Line Number:** 120 (approximate, verify in the actual file)

---

## Changes to `nginx.conf`

### Change 5
- **Updated Configuration:** Modified `/health` and `/metrics` endpoints.
- **File:** `nginx.conf`
```
server {
    listen 80;
    server_name localhost;
    root /usr/share/nginx/html;
    index index.html;

    # Serve static files
    location / {
        try_files $uri /index.html;
    }

    # Health check endpoint
    location /health {
        default_type application/json;
        return 200 '{"status": "ok"}';
    }

    # Metrics endpoint (returns mock Prometheus metrics)
    location /metrics {
        default_type text/plain;
        return 200 '# HELP http_requests_total Total number of HTTP requests\n# TYPE http_requests_total counter\nhttp_requests_total{method="get",route="/",status="200"} 10\n# HELP http_request_duration_seconds HTTP request duration in seconds\n# TYPE http_request_duration_seconds histogram\nhttp_request_duration_seconds_bucket{le="0.1"} 5\nhttp_request_duration_seconds_bucket{le="0.5"} 8\nhttp_request_duration_seconds_bucket{le="1"} 10\nhttp_request_duration_seconds_bucket{le="+Inf"} 10\nhttp_request_duration_seconds_sum 2.5\nhttp_request_duration_seconds_count 10';
    }

    # Error pages
    error_page 404 /index.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }
}
```

---

## Changes to `deployment.yaml`

### Change 6
- **Updated Configuration:** Adjusted deployment settings, including Prometheus annotations, ports, and container image.
- **File:** `deployment.yaml`

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: react-sre-app
  namespace: react-sre-app
  labels:
    app: react-sre-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: react-sre-app
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  template:
    metadata:
      labels:
        app: react-sre-app
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/port: "80"  # Fix: Match Nginx port
        prometheus.io/path: "/metrics"
    spec:
      containers:
      - name: react-sre-app
        image: vishnuvardhandommeti/react-sre-app:latest  # Ensure correct image
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 80  # Fix: Change from 3000 to 80
          name: http
        resources:
          limits:
            cpu: "500m"
            memory: "512Mi"
          requests:
            cpu: "200m"
            memory: "256Mi"
        readinessProbe:
          httpGet:
            path: /health
            port: 80  # Fix: Correct port
          initialDelaySeconds: 10
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /health
            port: 80
          initialDelaySeconds: 15
          periodSeconds: 20
        env:
        - name: NODE_ENV
          value: "production"
```
---

## Final Steps

After making these changes, run the following commands to apply them:
```bash
# Start Docker
sudo systemctl start docker || sudo service docker start

# Delete existing Minikube cluster
minikube delete

# Start Minikube
minikube start

# Run the deployment script
./deploy_sre_app.sh
```

This ensures that all updates take effect properly and the React SRE application is deployed successfully.
<img width="608" alt="image" src="https://github.com/user-attachments/assets/987c5cfa-a906-4644-ba99-09f1f9009cd7" />

## React-app
<img width="902" alt="image" src="https://github.com/user-attachments/assets/d63281d1-7ac2-4533-b4e7-54e9025883b8" />
<img width="347" alt="image" src="https://github.com/user-attachments/assets/4fcf444e-3f42-481f-920a-6adec9855027" />
<img width="304" alt="image" src="https://github.com/user-attachments/assets/c49433b7-013f-45ba-84b0-e747c2328370" />

## prometheus
<img width="952" alt="image" src="https://github.com/user-attachments/assets/16c95e5e-40bb-4b3d-af00-46de07a30617" />

## Graphana 
![image](https://github.com/user-attachments/assets/e63fe0d3-af3f-4e96-aae2-3911241782df)
