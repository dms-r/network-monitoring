# 🛰️ Docker-Based Network Monitoring Stack

This stack provides a complete network and infrastructure monitoring system using **Docker Compose**, featuring:

- **Prometheus** – metrics collection and alerting
- **Grafana** – visualization and dashboards
- **Node Exporter** – system-level metrics (CPU, memory, network)
- **Blackbox Exporter** – external endpoint monitoring (HTTP, ping)
- **cAdvisor** – Docker container metrics

---

## 🚀 Services Overview

| Service            | Port  | Description                                  |
|--------------------|-------|----------------------------------------------|
| Prometheus         | 9090  | Metrics collection & queries                 |
| Grafana            | 3000  | Metrics dashboards                           |
| Node Exporter      | 9100  | Host system metrics                          |
| Blackbox Exporter  | 9115  | HTTP/ping endpoint probe                     |
| cAdvisor           | 8080  | Docker container stats                       |

---

## 🛠️ Setup Instructions

### 1. Clone the Project

```bash
git clone https://github.com/your-org/network-monitoring-stack.git
cd network-monitoring-stack
````

### 2. Directory Structure

```
network-monitoring/
├── docker-compose.yml
├── prometheus/
│   ├── prometheus.yml
│   ├── alert.rules.yml
│   └── blackbox.yml
└── grafana/
```

### 3. Launch the Stack

```bash
docker-compose up -d
```

---

## 🌐 Accessing Services

* **Grafana**: [http://localhost:3000](http://localhost:3000)

  * Username: `admin`, Password: `admin` (change this in production)

* **Prometheus**: [http://localhost:9090](http://localhost:9090)

* **cAdvisor**: [http://localhost:8080](http://localhost:8080)

---

## 📊 Grafana Setup

### 1. Add Prometheus Data Source

* Navigate to **Configuration > Data Sources**
* Choose **Prometheus**
* URL: `http://prometheus:9090`

### 2. Import Dashboards

| Dashboard                    | ID     |
| ---------------------------- | ------ |
| Node Exporter Full           | `1860` |
| Docker Monitoring (cAdvisor) | `193`  |
| Blackbox Exporter Overview   | `7587` |

Go to **Dashboards > Import**, and paste the dashboard ID.

---

## 🔍 What is Monitored

### Node Exporter

* CPU, RAM, disk, load, network I/O

### Blackbox Exporter

* External HTTP response status, ping response time

### cAdvisor

* Docker container CPU, memory, network, filesystem stats

---

## 🚨 Alerting (Prometheus)

Example alert rule:

* **EndpointDown** – triggers if any probe from Blackbox fails for 1 minute

Defined in: `prometheus/alert.rules.yml`

You can extend this by integrating **Alertmanager**.

---

## 📌 Notes

* Prometheus scrapes services every **15 seconds**
* Add/remove endpoints to monitor by editing `prometheus.yml`
* This stack runs entirely in Docker and uses a `bridge` network

---

## ✅ Requirements

* Docker
* Docker Compose

---

## 📜 License

MIT License
