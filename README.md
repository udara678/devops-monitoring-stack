# 📊 DevOps Observability & Infrastructure Monitoring Stack

[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![Prometheus](https://img.shields.io/badge/Prometheus-v2.x-E6522C?style=flat-square&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-v10.x-F46800?style=flat-square&logo=grafana&logoColor=white)](https://grafana.com/)

A containerized, production-ready observability and infrastructure monitoring stack built with **Docker Compose**, **Prometheus**, **Node Exporter**, and **Grafana**. 

This stack scrapes host server metrics in real time and visualizes hardware health, resource consumption, and network saturation through pre-configured Grafana dashboards.

---

## 🏗️ Architecture & Data Flow

```
┌─────────────────┐       Scrapes /metrics (5s)       ┌─────────────────┐       Queries Metrics       ┌─────────────────┐
│  Node Exporter  │ ◄──────────────────────────────── │   Prometheus    │ ◄────────────────────────── │     Grafana     │
│   (Port 9100)   │                                   │   (Port 9090)   │                             │   (Port 3000)   │
└─────────────────┘                                   └─────────────────┘                             └─────────────────┘
  (Host OS Metrics:                                    (Time-Series TSDB                             (Real-Time Analytics
 CPU, RAM, Disk, Net)                                     Storage & Rules)                              Visual Dashboard)
```

1. **Node Exporter (`:9100`):** Lightweight collector container that extracts host machine hardware and OS metrics.
2. **Prometheus (`:9090`):** Time-series database that pulls (scrapes) collected metrics at 5-second intervals.
3. **Grafana (`:3000`):** Web-based data visualization platform presenting live CPU load, memory utilization, disk I/O, and network bandwidth.

---

## 🚀 Quick Start

### 1. Prerequisites
- [Docker](https://docs.docker.com/get-docker/) & [Docker Compose](https://docs.docker.com/compose/) installed and running.

### 2. Launch the Monitoring Stack
Clone the repository and run all services in detached mode:

```bash
git clone https://github.com/udara678/devops-monitoring-stack.git
cd devops-monitoring-stack
docker compose up -d
```

### 3. Verify Running Services
```bash
docker ps
```

| Service | Container Name | Port Mapping | Access URL |
| :--- | :--- | :--- | :--- |
| **Prometheus TSDB** | `prometheus` | `9090:9090` | [http://localhost:9090](http://localhost:9090) |
| **Grafana Dashboard** | `grafana` | `3000:3000` | [http://localhost:3000](http://localhost:3000) |
| **Node Exporter** | `node_exporter` | `9100:9100` | [http://localhost:9100/metrics](http://localhost:9100/metrics) |

---

## 📈 Grafana Configuration & Dashboard Setup

1. Open your browser and navigate to **`http://localhost:3000`**.
2. Log in using default credentials:
   - **Username:** `admin`
   - **Password:** `admin`
3. Add Prometheus as a Data Source:
   - Navigate to **Connections** ➔ **Data sources** ➔ **Add data source** ➔ **Prometheus**.
   - Set Prometheus server URL: `http://prometheus:9090`.
   - Click **Save & test**.
4. Import Pre-built Dashboard:
   - Go to **Dashboards** ➔ **Import dashboard**.
   - Enter Dashboard ID **`1860`** (*Node Exporter Full*) and click **Load**.
   - Select the `Prometheus` datasource and click **Import**.

---

## 🛠️ Tech Stack & Key Concepts
- **Container Orchestration:** Docker Compose multi-container networking
- **Observability:** Prometheus Pull Architecture, Metric Scraping, TSDB
- **Visualization:** Grafana Panels, Node Exporter Dashboards, Alert Thresholds
- **Host Metrics Monitored:** CPU Pressure & Utilization, RAM/Swap Usage, Disk I/O & Storage Capacity, Network Traffic Throughput

---

## 👤 Author
**K.A. Udara Hansana Kodikara**  
IT Undergraduate | Aspiring DevOps Engineer  
🔗 [LinkedIn](https://linkedin.com/in/udara-hansana) · 💻 [GitHub](https://github.com/udara678) · 🌐 [Portfolio](https://udara678.github.io)
