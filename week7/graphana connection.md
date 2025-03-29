# Connecting Django BankingSystem to Grafana and Prometheus

## **Why Use Grafana and Prometheus?**
- **Prometheus**: Collects and stores metrics from the Django application.
- **Grafana**: Visualizes the collected metrics from Prometheus.

---

## **Step-by-Step Setup**

### **1. Install and Configure Prometheus**

#### **Install Prometheus**
```bash
sudo apt update
sudo apt install prometheus
```
Or manually download it:
```bash
wget https://github.com/prometheus/prometheus/releases/latest/download/prometheus-*.linux-amd64.tar.gz
tar -xvf prometheus-*.tar.gz
cd prometheus-*
```

#### **Configure Prometheus to Scrape Django Metrics**
- Create a new file: `/etc/prometheus/prometheus.yml`
- Add the following configuration:
```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'django'
    static_configs:
      - targets: ['localhost:8000']
```
- If Django runs on another port, update `targets` accordingly.

#### **Run Prometheus**
```bash
./prometheus --config.file=prometheus.yml
```

---

### **2. Install and Configure Django-Prometheus**

#### **Install the package**
```bash
pip install django-prometheus
```

#### **Update `settings.py`**
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    # other apps...
    'django_prometheus',
]

MIDDLEWARE = [
    'django_prometheus.middleware.PrometheusBeforeMiddleware',
    # other middleware...
    'django_prometheus.middleware.PrometheusAfterMiddleware',
]
```

#### **Update `urls.py` to Expose Metrics**
```python
from django.urls import path, include

urlpatterns = [
    # other routes...
    path('', include('django_prometheus.urls')),
]
```
- Metrics will be available at: `http://localhost:8000/metrics`

---

### **3. Install and Configure Grafana**

#### **Install Grafana**
```bash
sudo apt install -y grafana
```
Or manually:
```bash
wget https://dl.grafana.com/oss/release/grafana_8.3.3_amd64.deb
sudo dpkg -i grafana_8.3.3_amd64.deb
```

#### **Start Grafana**
```bash
sudo systemctl start grafana-server
```

#### **Open Grafana**
- Visit: `http://localhost:3000`
- Default credentials:
  - **Username**: `admin`
  - **Password**: `admin` (change on first login)

#### **Add Prometheus as a Data Source**
- Go to **Configuration → Data Sources**
- Click **Add Data Source**
- Select **Prometheus**
- Set **URL**: `http://localhost:9090`
- Click **Save & Test**

#### **Create Dashboards**
- Go to **Dashboards → New Dashboard**
- Add a new **Panel**
- Query example:
```promql
http_requests_total
```
- Save and view the metrics.

---

## **Final Steps**
- Ensure **Django**, **Prometheus**, and **Grafana** are running.
- Check Prometheus metrics at `http://localhost:8000/metrics`.
- Verify Prometheus is collecting data at `http://localhost:9090`.
- Visualize the data in Grafana.

### 🎯 Now your **BankingSystem** project is successfully connected to Grafana and Prometheus!

