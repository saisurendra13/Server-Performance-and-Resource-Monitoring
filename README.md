# Server Performance and Resource Monitoring

> A real-time Linux server monitoring and analytics project built using Raspberry Pi, Python, SQLite, Bash, Cron Jobs, GitHub Automation, Jupyter Notebook, SQL, and Power BI.

Developed collaboratively by:

- **Sai Surendra Munagala** — Infrastructure, Monitoring & Backend Automation
- **Shaik Seema Kousar** — Data Analytics, SQL & Power BI Dashboard

---

# Project Overview

Server Performance and Resource Monitoring is a production-style infrastructure monitoring project designed to continuously track server resource usage in real time.

The project collects live system metrics from a Raspberry Pi Linux server, stores them in structured formats, automates database loading and GitHub synchronization, and provides analytics dashboards for monitoring server health and performance trends.

The system helps identify:

- High CPU utilization spikes
- Excessive RAM consumption
- Disk usage trends
- Server performance bottlenecks
- Resource growth patterns over time

---

# System Architecture

```text
Raspberry Pi Linux Server
        │
        ├── collect.py
        ├── alert.py
        ├── check_health.sh
        └── load_to_db.py
        │
        ▼
CSV + SQLite Database
        │
        ▼
GitHub Auto Sync
        │
        ▼
Jupyter Notebook + SQL Analysis
        │
        ▼
Power BI Dashboard
```

---

# Project Workflow

## Infrastructure Layer (Sai's Work)

The Raspberry Pi server continuously monitors:

- CPU usage
- RAM usage
- Disk usage

using Python scripts, Linux commands, and cron jobs.

The monitoring system:

- Collects metrics every minute
- Stores data into CSV files
- Loads data into SQLite database hourly
- Performs automated threshold checks
- Pushes updated data to GitHub automatically

---

## Analytics & Dashboard Layer (Seema's Work)

The analytics layer uses:

- Python
- Pandas
- SQL
- Jupyter Notebook
- Power BI

to analyze monitoring data and visualize server performance trends.

The dashboard provides:

- KPI cards
- Resource trend analysis
- CPU spike analysis
- Historical monitoring insights
- Interactive visual reports

---

# Project Structure

```text
Server-Performance-and-Resource-Monitoring/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── scripts/
│   ├── collect.py
│   ├── load_to_db.py
│   ├── check_health.sh
│   └── alert.py
│
├── data/
│   ├── metrics.csv
│   └── metrics.db
│
├── analysis/
│   └── seema_analysis.ipynb
│
└── powerbi/
    └── server_monitoring_dashboard.pbix
```

---

# Features

# Real-Time Monitoring
- Live CPU usage tracking
- Live RAM usage tracking
- Live Disk usage tracking
- Automated metric collection every 60 seconds

# Data Storage
- CSV-based logging
- SQLite database integration
- Historical metric storage

# Alert Monitoring
- CPU threshold alerts
- RAM threshold alerts
- Disk usage threshold alerts

# Automation
- Cron job scheduling
- Hourly GitHub auto-push
- Automated database loading

# Analytics & Visualization
- SQL-based analysis
- Jupyter Notebook EDA
- Power BI dashboards
- KPI monitoring

---

# Technologies Used

| Category | Technologies |
|---|---|
| Operating System | Raspberry Pi OS (Linux) |
| Programming | Python 3, Bash |
| Libraries | psutil, pandas, sqlalchemy |
| Automation | Cron Jobs |
| Database | SQLite |
| Monitoring | Netdata |
| Analytics | Pandas, SQL, Jupyter Notebook |
| Visualization | Power BI Desktop |
| Version Control | Git & GitHub |

---

# Infrastructure Monitoring (Sai's Contribution)

## Monitoring Scripts

| Script | Purpose |
|---|---|
| `collect.py` | Collects CPU, RAM & Disk metrics every minute |
| `alert.py` | Generates alerts based on thresholds |
| `load_to_db.py` | Loads CSV data into SQLite database |
| `check_health.sh` | Linux Bash-based system health checker |

---

## Cron Job Automation

```bash
* * * * * /usr/bin/python3 /home/pi/Server-Performance-and-Resource-Monitoring/scripts/collect.py >> /home/pi/cron.log 2>&1

*/5 * * * * /usr/bin/python3 /home/pi/Server-Performance-and-Resource-Monitoring/scripts/alert.py >> /home/pi/alerts.log 2>&1

0 * * * * /usr/bin/python3 /home/pi/Server-Performance-and-Resource-Monitoring/scripts/load_to_db.py >> /home/pi/cron.log 2>&1

5 * * * * cd /home/pi/Server-Performance-and-Resource-Monitoring && git pull origin main --quiet && git add data/metrics.csv data/metrics.db && git commit -m "Auto Update $(date '+\%Y-\%m-\%d \%H:\%M')" && git push origin main >> /home/pi/cron.log 2>&1
```

---

# Live Monitoring with Netdata

Netdata provides live server visualization.

## Access from Raspberry Pi

```text
http://localhost:19999
```

## Access from Local Network

```text
http://192.168.1.31:19999
```

Features:
- Real-time CPU monitoring
- Live RAM tracking
- Network activity monitoring
- Disk usage visualization
- Refresh every 3 seconds

---

# Power BI Dashboard (Seema's Contribution)

## Dashboard Overview

The Power BI dashboard visualizes server performance metrics collected from the Raspberry Pi monitoring system.

It helps identify:

- Resource bottlenecks
- CPU spikes
- Memory pressure
- Performance trends
- Server health patterns

---

# Dashboard KPI Cards

| KPI | Description |
|---|---|
| Avg CPU % | Average CPU utilization |
| Max Disk % | Maximum recorded disk usage |
| High CPU Count | Number of times CPU crossed threshold |
| Total Readings | Total monitoring records collected |

---

# Dashboard Visualizations

## 📋 Data Table
Displays raw monitoring data including:
- CPU %
- RAM %
- Disk %
- Timestamp

---

## 📈 CPU, RAM & Disk Usage Over Time
Line chart showing system resource trends across multiple days.

Used for:
- Trend analysis
- Peak usage identification
- Resource comparison

---

## 📈 CPU Usage Trend Analysis
Shows cumulative CPU usage over time.

Helps identify:
- High-load periods
- Increasing server demand
- Performance degradation trends

---

## 📊 High CPU Count by Day
Displays number of critical CPU spikes per day.

Useful for:
- Detecting unstable periods
- Troubleshooting heavy workloads
- Capacity planning

---

# DAX Measures Used

```DAX
-- Average CPU %
Avg CPU % = AVERAGE(metrics[cpu_percent])

-- Max Disk %
Max Disk % = MAX(metrics[disk_percent])

-- High CPU Count
High CPU Count =
CALCULATE(
    COUNT(metrics[cpu_percent]),
    metrics[cpu_percent] > 80
)

-- Total Readings
Total Readings = COUNT(metrics[timestamp])
```

---

# Key Insights from Dashboard

- ⚠️ RAM usage remained consistently high between 89–92%
- 🔴 CPU crossed critical threshold multiple times
- ✅ Disk usage remained stable around 25%
- 📈 CPU utilization increased steadily over monitoring period
- 📊 Historical data helped identify resource consumption trends

---

# Sample Dataset

```csv
timestamp,cpu_percent,ram_percent,disk_percent
2026-05-16 12:18:25,0.8,58.7,22.8
2026-05-16 12:18:26,0.8,58.8,22.8
2026-05-16 12:18:27,0.8,58.9,22.8
```

---

# Installation

## Clone Repository

```bash
git clone https://github.com/saisurendra13/Server-Performance-and-Resource-Monitoring.git
```

---

## Move into Project Directory

```bash
cd Server-Performance-and-Resource-Monitoring
```

---

## Install Dependencies

```bash
pip3 install -r requirements.txt
```

---

# Current Project Status

| Component | Status |
|---|---|
| Real-Time Monitoring | Completed |
| CSV Logging | Completed |
| SQLite Database | Completed |
| Alert System | Completed |
| Cron Automation | Completed |
| GitHub Automation | Completed |
| SQL Analysis | Completed |
| Jupyter Notebook EDA | Completed |
| Power BI Dashboard | Completed |

---

# Future Enhancements

- Email notification alerts
- Grafana integration
- Docker container deployment
- AWS cloud deployment
- Multi-server monitoring support
- Predictive analytics using Machine Learning
- Real-time web dashboard

---

# Contributors

| Name | Role |
|---|---|
| Sai Surendra Munagala | Infrastructure, Monitoring & Backend Automation |
| Shaik Seema Kousar | Data Analytics, SQL & Power BI Dashboard |

---

# License

This project is developed for educational, learning, and portfolio purposes.
