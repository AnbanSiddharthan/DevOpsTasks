## Install Prometheus and Grafana on a Linux EC2 machine, connect Prometheus to Grafana, and create a dashboard to view metrics.

### Step 1 — Install Node Exporter

```bash
sudo apt update
sudo apt install prometheus-node-exporter -y
```

```bash
sudo systemctl status prometheus-node-exporter
```

```bash
curl http://localhost:9100/metrics
```
### Step 2 — Install Prometheus

```bash
sudo apt install prometheus -y
```

```bash
sudo systemctl status prometheus
```

```bash
sudo systemctl status prometheus
```
### Step 4 — Configure Prometheus

```bash
sudo nano /etc/prometheus/prometheus.yml
```
#### CONFIGS
```bash
scrape_configs:

  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["localhost:9100"]
```


### Step 4 — Check Prometheus

#### URL 

```bash
http://YOUR_EC2_PUBLIC_IP:9090
```
<img width="1917" height="897" alt="image" src="https://github.com/user-attachments/assets/0b1074a3-006e-47f3-9532-c8e1ee140234" />

### Step 5 - Install Grafana

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https software-properties-common wget
```


```bash
sudo mkdir -p /etc/apt/keyrings
```

```bash
wget -q -O - https://apt.grafana.com/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/grafana.gpg
```

```bash
sudo apt-get install grafana -y
```


```bash
sudo systemctl enable grafana-server
```
### Step 6 — Open Grafana

#### Browser url

```bash
http://YOUR_EC2_PUBLIC_IP:3000
```
<img width="1917" height="900" alt="image" src="https://github.com/user-attachments/assets/92724cd6-17c6-41c2-8e04-d12875502263" />

### Result Screenshots

<img width="1917" height="907" alt="image" src="https://github.com/user-attachments/assets/a644d4c4-406f-4df9-afb7-3acef91f9b0e" />

<img width="1468" height="500" alt="image" src="https://github.com/user-attachments/assets/12c53448-1e51-41ee-b3da-680f9c56df78" />

<img width="1471" height="753" alt="image" src="https://github.com/user-attachments/assets/555048a6-5cfc-4e7b-8df3-f014dfc3f3d6" />

<img width="1470" height="442" alt="image" src="https://github.com/user-attachments/assets/1e107a01-1699-4361-bcb7-56d861b7cd4f" />
