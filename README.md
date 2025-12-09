# Prometheus + Grafana Monitoring Lab

## Project Overview
This project demonstrates a real-world monitoring setup using Prometheus, Node Exporter, and Grafana on an AWS EC2 Ubuntu server.  
It showcases practical Cloud and DevOps skills through hands-on implementation.

## Architecture

Internet  
↓  
AWS EC2 (Ubuntu)  
↓  
Node Exporter → Prometheus → Grafana  

## Tech Stack
AWS EC2       : Cloud Virtual Machine  
Ubuntu 22.04  : Operating System  
Prometheus    : Metrics Collection  
Node Exporter : System Metrics Exporter  
Grafana       : Data Visualization  
Git + GitHub  : Version Control  

## Project Structure

prometheus-grafana-monitoring-lab/
|
|-- configs/
|   └── prometheus/
|       └── prometheus.yml
|
|-- dashboards/
|   └── node-exporter-dashboard.json
|
|-- systemd/
|   ├── prometheus.service
|   ├── node_exporter.service
|   └── grafana-server.service
|
└── .gitignore

## Setup Instructions

### Step 1: Update System
sudo apt update && sudo apt upgrade -y

### Step 2: Install Prometheus
sudo useradd --no-create-home --shell /bin/false prometheus  
wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz  
tar -xvf prometheus-2.52.0.linux-amd64.tar.gz  
sudo mv prometheus-2.52.0.linux-amd64 /etc/prometheus  

### Step 3: Install Node Exporter
sudo useradd --no-create-home --shell /bin/false node_exporter  
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz  
tar -xvf node_exporter-1.7.0.linux-amd64.tar.gz  
sudo mv node_exporter-1.7.0.linux-amd64 /etc/node_exporter  

### Step 4: Install Grafana
sudo apt install -y apt-transport-https software-properties-common  
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -  
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"  
sudo apt update  
sudo apt install grafana -y  

## Service Management

sudo systemctl daemon-reload  

sudo systemctl start prometheus  
sudo systemctl enable prometheus  

sudo systemctl start node_exporter  
sudo systemctl enable node_exporter  

sudo systemctl start grafana-server  
sudo systemctl enable grafana-server  

## Access URLs

Prometheus: http://<EC2-PUBLIC-IP>:9090  
Grafana:    http://<EC2-PUBLIC-IP>:3000  

Default Grafana Login:  
Username: admin  
Password: admin  

## Dashboard
Import the following file in Grafana:
dashboards/node-exporter-dashboard.json

## Best Practices
- Large binaries are excluded using .gitignore
- Clean and production-like file structure
- Systemd-based service management

## Author
Ramkumar Baghel  
GitHub: https://github.com/webcreaterRam
