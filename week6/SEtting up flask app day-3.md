# Grafana Dashboards and SRE Concepts

## Latency – How long it takes to serve a customer

- **Example:** A customer orders a burger. The time from placing the order to receiving the burger is latency.
- **In tech:** It's the time it takes for a user to get a response after making a request.
  - If latency is high, customers (users) will get frustrated.

## Traffic – How many customers are coming in per hour

- **Example:** A counter at the restaurant door clicks every time a customer walks in.
- **In tech:** Counting how many requests the system gets per second or minute.
  - If traffic is too high, the system might struggle to keep up.

## Errors – How many orders are wrong or complaints received

- **Example:** If customers send food back because it’s cold or incorrect, that’s an error.
- **In tech:** Tracking HTTP errors like 500 (server error) means something’s wrong with the system.
  - More errors mean a bad user experience.

## Saturation – How close the restaurant is to full capacity

- **Example:** If the restaurant has 50 tables and 49 are occupied, it's almost full — that’s high saturation.
- **In tech:** Tracking how many requests are being processed at the same time.
  - If the system is saturated, performance will drop.

# Observability

## Metrics – Tracking key numbers

- **Example:** A pilot monitors altitude, speed, and fuel level.
- **In tech:** Metrics track system performance — like how long requests take and how many are successful.

## Logs – Recording detailed events

- **Example:** A flight recorder (black box) logs everything that happens on the plane.
- **In tech:** Logs record every request, error, and system event — useful for debugging.

## Visualization – Easy-to-read dashboard

- **Example:** The cockpit dashboard shows altitude, speed, and warnings in one place.
- **In tech:** Dashboards make it easy to see how the system is performing.

## Instrumentation – Adding sensors to track performance

- **Example:** Sensors on the plane track fuel level and engine temperature.
- **In tech:** Adding code to measure how the app behaves under different loads.

# Health Monitoring

## Liveness Probes – Checking if the patient is alive

- **Example:** A pulse check — is the patient breathing?
- **In tech:** A simple check to see if the app is running at all.

## Readiness Probes – Checking if the patient can perform activities

- **Example:** Can the patient walk and talk?
- **In tech:** A check to see if the app is ready to handle requests.

## Health Endpoints – Checking specific health stats

- **Example:** Checking blood pressure, temperature, and oxygen levels.
- **In tech:** Different health checks for different parts of the app (like memory and database).

## Dependency Checks – Are all organs working together?

- **Example:** Heart, lungs, and brain need to work together.
- **In tech:** The app needs to connect to the database and other services to work properly.

# Service Level Objectives

## Error Rate Tracking – How many pizzas are wrong

- **Example:** Out of 100 pizzas, 5 are wrong — that’s a 5% error rate.
- **In tech:** Tracking how many requests fail or result in errors.

## Latency Histograms – How long deliveries take

- **Example:** 70% of pizzas arrive in under 20 minutes, 25% take 30 minutes, and 5% take an hour.
- **In tech:** A histogram shows how fast most requests are processed.

## Request Success Rate – Percentage of successful deliveries

- **Example:** 95% of pizzas were delivered correctly and on time.
- **In tech:** Measures how many requests are processed successfully.

# Running the Script

- Run the script using:
  ```sh
  ./lightweight-sre-monitoring.sh
  ```
- If there is a Docker permission error, run:
  ```sh
  sudo dockerd
  ```
- If a permission error occurs, modify the script permissions:
  ```sh
  chmod 777 lightweight-sre-monitoring.sh
  ```
- If you encounter a `--short` error, remove `--short` from the script after `kubectl`.
- If a timeout error occurs, increase the time from `120` to `200` in the script.
- After successfully running, open the Grafana dashboard at:
  ```
  http://localhost:3000
  ```
![image](https://github.com/user-attachments/assets/f1e48f70-ff8d-495e-9cba-162b0ffd4863)
<img width="299" alt="image" src="https://github.com/user-attachments/assets/b5f7b4b9-8255-43b2-9ac0-38da1e98d75c" />

# Creating Dashboards and Panels

- **Step 1:** Go to Dashboards → Add New Dashboard → Add Visualization
- **Step 2:** Select Prometheus as the data source
- **Step 3:** Select visualization type (e.g., Stat, Time Series, Bar Chart)
- **Step 4:** Enter queries:

### Panel 1: Request Rate per Endpoint (Stat Visualization)
```promql
sum by(endpoint) (rate(app_request_count_total{namespace="sre-demo"}[24h]))
```

### Panel 2: HTTP 5xx Error Rate (Stat Visualization)
```promql
sum(rate(app_request_count{namespace="sre-demo", http_status=~"5.."}[1m])) / sum(rate(app_request_count{namespace="sre-demo"}[1m])) * 100
```

### Panel 3: Active Requests (Stat Visualization)
```promql
app_active_requests{namespace="sre-demo"}
```

### Panel 4: 95th Percentile Request Latency (Time Series Visualization)
```promql
histogram_quantile(0.95, sum(rate(app_request_latency_seconds_bucket{namespace="sre-demo"}[5m])) by (le, endpoint))
```

### Panel 5: Total Requests Count (Stat Visualization)
```promql
app_request_latency_seconds_count{namespace="sre-demo"}
```

### Panel 6: Kubernetes API Server Cache List Operations (Bar Chart)
```promql
rate(apiserver_cache_list_total{job="kubernetes-apiservers"}[5m])
```

### Panel 7: Total Cache List Operations (Gauge Visualization)
```promql
sum(apiserver_cache_list_total{job="kubernetes-apiservers"})
```
## Prometheus Dashboard Queries

### 1. Total Number of Requests (Counter)
**Query:**
```promql
sum(app_request_count_total)
```
**Visualization:**
- Stat Panel (to show a single numeric value)
- Time-Series Graph (to observe trends over time)

### 2. Requests Per Endpoint (Bar Chart)
**Query:**
```promql
sum by (endpoint) (app_request_count_total)
```
**Visualization:**
- Bar Chart (to compare requests per endpoint)

### 3. Request Latency Over Time
**Query:**
```promql
rate(app_request_latency_seconds_sum[5m]) / rate(app_request_latency_seconds_count[5m])
```
**Visualization:**
- Time-Series Graph (to observe latency trends over time)

### 4. Error Rate (Percentage)
**Query:**
```promql
(sum(app_error_count_total) / sum(app_request_count_total)) * 100
```
**Visualization:**
- Gauge (to display the error percentage)
- Time-Series Graph (to observe error rate fluctuations)

### 5. CPU Usage Over Time
**Query:**
```promql
rate(process_cpu_seconds_total[5m])
```
**Visualization:**
- Time-Series Graph (to track CPU usage trends)

### 6. Memory Usage
**Query:**
```promql
process_resident_memory_bytes
```
**Visualization:**
- Gauge (for current memory usage)
- Time-Series Graph (for trends)

### 7. Active Requests
**Query:**
```promql
app_active_requests
```
**Visualization:**
- Gauge (to see how many requests are being processed at a time)
- Time-Series Graph (to track changes over time)

### 8. Requests per HTTP Status Code
**Query:**
```promql
sum by (http_status) (app_request_count_total)
```
**Visualization:**
- Pie Chart (to show the proportion of different status codes)
- Bar Chart (to compare counts)
### Saving Dashboard
- Click **Save Dashboard** → Name it `SRE Basic Dashboard`

# Log Analysis using Loki

- **Step 1:** Create a new dashboard and add panels
- **Step 2:** Select **Loki** as the data source
- **Step 3:** Choose visualization type and enter queries:

### Panel 1: Filter Logs for `sre-demo` Namespace (Logs Visualization)
```logql
{namespace="sre-demo"}
```

### Panel 2: Filter Logs for Errors (Stat Visualization)
```logql
{namespace="sre-demo"} |= `Error`
```

### Panel 3: Log Count over Time (Stat Visualization)
```logql
sum(count_over_time({namespace="sre-demo"}[1m]))
```

### Saving Dashboard
- Click **Save Dashboard** → Name it `Log Analysis`
<img width="757" alt="image" src="https://github.com/user-attachments/assets/c6adfe45-b28a-4ecb-9e04-a99933fd167f" />
<img width="758" alt="image" src="https://github.com/user-attachments/assets/94027aa8-b5dc-4b92-8461-c193e0b2229d" />


### Flask-APP
Commands:
## Docker and Kubernetes Commands with Explanation

### 1. Build Docker Image
```sh
docker build -t sre-flask-app:latest .
```
**Explanation:**
- `docker build` → Command to build a Docker image.
- `-t sre-flask-app:latest` → Tags the image with the name `sre-flask-app` and the `latest` tag.
- `.` → Uses the current directory as the build context.

### 2. Restart Kubernetes Deployment
```sh
kubectl rollout restart deployment sre-flask-app -n sre-demo
```
**Explanation:**
- `kubectl rollout restart` → Restarts a Kubernetes deployment.
- `deployment sre-flask-app` → Specifies the deployment name (`sre-flask-app`).
- `-n sre-demo` → Targets the `sre-demo` namespace.

### 3. Port Forward Kubernetes Service
```sh
kubectl port-forward svc/sre-flask-app 8081:80 -n sre-demo
```
**Explanation:**
- `kubectl port-forward` → Forwards a local port to a service in Kubernetes.
- `svc/sre-flask-app` → Specifies the service name (`sre-flask-app`).
- `8081:80` → Maps local port `8081` to container port `80`.
- `-n sre-demo` → Targets the `sre-demo` namespace.

### 4. Configure Docker to Use Minikube’s Docker Daemon
```sh
eval $(minikube docker-env)
```
**Explanation:**
- `minikube docker-env` → Outputs environment variables for using Minikube’s Docker daemon.
- `eval $(...)` → Evaluates and applies these environment variables to the current shell session.

### 5. Get All Pods in the Monitoring Namespace
```sh
kubectl get pods -n monitoring
```
**Explanation:**
- `kubectl get pods` → Lists all running pods in Kubernetes.
- `-n monitoring` → Filters the results to the `monitoring` namespace.

### 6. Port Forward Prometheus Pushgateway
```sh
kubectl port-forward prometheus-prometheus-pushgateway-544579d549-q8g7g 9091 -n monitoring
```
**Explanation:**
- `kubectl port-forward` → Forwards a local port to a pod in Kubernetes.
- `prometheus-prometheus-pushgateway-544579d549-q8g7g` → Specifies the pod name.
- `9091` → Maps local port `9091` to the container’s default port.
- `-n monitoring` → Targets the `monitoring` namespace.


<img width="559" alt="image" src="https://github.com/user-attachments/assets/aebb915f-f260-4e1a-a5fd-ed4e02270d88" />
<img width="547" alt="image" src="https://github.com/user-attachments/assets/ae0324fc-6147-472c-920f-b1e35ff8b37a" />
<img width="493" alt="image" src="https://github.com/user-attachments/assets/259fd2e1-0cc0-4275-996f-14595a72df2d" />

## localhost:8080
<img width="677" alt="image" src="https://github.com/user-attachments/assets/28a208c8-2cf3-427a-af73-ce97994de081" />
![Users]
<img width="550" alt="image" src="https://github.com/user-attachments/assets/db64668f-4203-41b1-978b-da451939b456" />
![Slow]
<img width="310" alt="image" src="https://github.com/user-attachments/assets/cd283341-99aa-474b-8681-759a67ac05ae" />
![Metrics]
<img width="535" alt="image" src="https://github.com/user-attachments/assets/97c963ad-fc31-4d09-8a7e-0eb670b9a248" />
[New dashboard-1742370827591.json](https://github.com/user-attachments/files/19346756/New.dashboard-1742370827591.json)

# Final Steps
- Reviewed all concepts in the afternoon session
- Prepared for the Python exam using LMS
