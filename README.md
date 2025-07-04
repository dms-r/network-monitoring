# 📡 Network & System Monitoring with Docker (Grafana + Prometheus)

This project sets up a **Docker-based monitoring stack** using:

- **Prometheus** – time series database for metrics
- **Node Exporter** – exposes host system metrics
- **cAdvisor** – collects Docker container metrics
- **Grafana** – dashboards and visualizations

---

## 🧱 Stack Components

| Service        | Port   | Description                                  |
|----------------|--------|----------------------------------------------|
| Grafana        | `3000` | Web UI for dashboards                        |
| Prometheus     | `9090` | Metrics database and query engine            |
| Node Exporter  | `9100` | Collects host CPU, memory, disk, network     |
| cAdvisor       | `8080` | Exposes metrics for running Docker containers|

---

## 📁 File Structure

```bash
network-monitoring/
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
├── grafana/
│   └── (optional: dashboards/provisioning)
└── README.md  <-- This file
```

---

## 🚀 How to Run

### 1. Clone the Repo

```bash
git clone https://github.com/yourname/network-monitoring.git
cd network-monitoring
```

### 2. Start the Stack

```bash
docker-compose up -d
```

### 3. Access Web Interfaces

| Tool      | URL                         | Default Login       |
|-----------|-----------------------------|----------------------|
| Grafana   | http://localhost:3000       | `admin` / `admin`    |
| Prometheus| http://localhost:9090       | _No login required_  |
| cAdvisor  | http://localhost:8080       | _No login required_  |

---

## 🔧 Configuration

### prometheus/prometheus.yml

Defines scrape jobs for:

- Prometheus itself
- Node Exporter (host system)
- cAdvisor (container-level metrics)

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['prometheus:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']

  - job_name: 'cadvisor'
    static_configs:
      - targets: ['cadvisor:8080']
```

---

## 📊 Grafana Dashboards

After login to Grafana:

1. Add Prometheus data source:
   - URL: `http://prometheus:9090`
2. Import dashboards from Grafana.com:
   - **Node Exporter Full** – ID: `1860`
   - **Docker / cAdvisor Metrics** – ID: `193`

---

## 📦 Docker Volumes & Permissions

Make sure the Node Exporter and cAdvisor services have access to your host’s `/proc`, `/sys`, and `/var/lib/docker` directories.

They’re mounted like this:

```yaml
volumes:
  - /proc:/host/proc:ro
  - /sys:/host/sys:ro
  - /:/rootfs:ro
  - /var/lib/docker/:/var/lib/docker:ro
```

This allows the monitoring stack to see real system and container metrics.

---

## 🧼 Stop & Clean

To stop and remove all containers:

```bash
docker-compose down
```

To remove volumes:

```bash
docker-compose down -v
```

---

## ✅ Optional Enhancements

- Alerting with Prometheus Alertmanager
- Email or Slack notifications
- Nginx reverse proxy with SSL
- Auto dashboard provisioning in Grafana

---

## 🛠️ Requirements

- Docker
- Docker Compose

Tested on Linux and macOS.

---

## 🧑‍💻 Author
Made by Dimas
Feel free to customize for your infrastructure.

