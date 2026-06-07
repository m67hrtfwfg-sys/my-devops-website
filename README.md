# Automated Cloud Infrastructure & Full-Stack Monitoring Ecosystem

A production-ready DevOps and Cloud Engineering project featuring automated cloud infrastructure provisioning, containerized application deployment, and continuous full-stack observability with real-time alerting.

---

## 🏗️ System Architecture
## 🏗️ System Architecture

```text
 [ GitHub Actions (CI/CD) ]
            │
            ▼ (SSH Deployment)
 ┌────────────────────────────────────────────────────────┐
 │ AWS Cloud (eu-north-1 Region)                          │
 │  └─► Custom VPC & Security Groups                      │
 │       └─► Ubuntu EC2 Instance                          │
 │            │                                           │
 │            ├──► [ Nginx Website Container ] ◄──┐       │
 │            │                                   │       │
 │            │      (Probes Uptime)              │       │
 │            ├──► [ Blackbox Exporter ] ─────────┘       │
 │            │          ▲                                │
 │            │          │ (Scrapes Metrics)              │
 │            ├──► [ Prometheus TSDB ]                    │
 │            │          ▲                                │
 │            │          │ (Queries Metrics)              │
 │            └──► [ Grafana Dashboard ]                  │
 └───────────────────────┬────────────────────────────────┘
                         │
                         ▼ (Triggers Alert Webhook)
                 [ Telegram Bot API ]

                 
This ecosystem is split into three main layers:
1. Infrastructure as Code (IaC): Automated AWS infrastructure provisioning using CloudFormation templates.
2. Containerized Deployment: Microservices managed and orchestrated using Docker and Docker Compose.
3. Observability & Alerting: Continuous telemetry collection via Prometheus and Blackbox Exporter, visualized in Grafana with integrated real-time notifications.

---

## 🛠️ Tech Stack & Tools

*   Cloud Provider: AWS (EC2, VPC, Security Groups, IAM, S3)
*   Infrastructure as Code: AWS CloudFormation
*   Containerization & Orchestration: Docker, Docker Compose
*   Observability: Prometheus, Grafana, Blackbox Exporter
*   Automation/Scripting: Python, Nginx
*   Alerting Channel: Telegram Bot Webhooks

---

## 🚀 Key Features

*   Infrastructure-as-Code: Entire network topology (VPC, Subnets, Security Groups) and compute resources are fully defined in code, ensuring immutable and reproducible cloud deployments.
*   Automated Continuous Integration: Connected through a CI/CD pipeline (ci-cd.yml) to ensure code changes are linted, tested, and automatically prepared for seamless delivery.
*   Blackbox Probing & Custom Telemetry: Uses a custom Python metric exporter combined with Prometheus Blackbox Exporter to monitor endpoint availability, HTTP status codes, and latencies from the outside in.
*   Enterprise-Grade Dashboards: Customized Grafana dashboards to monitor server hardware metrics (CPU, RAM, Storage) side-by-side with application uptime.
*   Instant Alerting Matrix: Pre-configured alerting rules (probe_success == 0) that trigger instant Telegram notifications via secure API webhooks within 1 minute of any service downtime.

---

## 📊 Observability in Action

### Grafana Live Monitoring Dashboard
*(Tip: Take a high-quality screenshot of your Grafana dashboard showing the graphs and paste it below)*
![Grafana Dashboard]<img width="1163" height="831" alt="Screenshot 2026-06-07 at 15 35 06" src="https://github.com/user-attachments/assets/07615fdf-ca8e-4dbb-a245-6c9dff0a2973" />


### Real-Time Telegram Downtime Alert
*(Tip: Take a screenshot of the alert message your bot sent to your Telegram phone/desktop and paste it below)*
![Telegram Alert]<img width="571" height="736" alt="Screenshot 2026-06-07 at 15 38 55" src="https://github.com/user-attachments/assets/928c1060-daf4-4459-884d-09e986f1b858" />


---

## 📦 Project Structure

`text
├── .github/
│   └── workflows/
│       └── ci-cd.yml             # CI/CD Pipeline Configuration
├── aws/
│   └── cloudformation-template.yml # Infrastructure as Code template
├── prometheus/
│   └── prometheus.yml            # Prometheus Scrape Configurations
├── src/
│   └── monitoring_agent.py       # Custom Python Metrics Exporter
├── docker-compose.yml            # Multi-container Docker orchestrator
└── README.md                     # Project Documentation

## ⚙️ HOW TO DEPLOY THIS INFRASTRUCTURE

​ 1. Provision AWS Resources: Deploy the CloudFormation stack using the AWS CLI or Console:
      bash:
      aws cloudformation create-stack --stack-name DevOps-Automation-Server --template-body file://aws/cloudformation-template.yml
 2. Launch the Containerized Stack:
    SSH into your EC2 instance and spin up the microservices:
      bash:
      sudo docker compose up -d
 3. Verify Alerting: Ensure Prometheus is successfully scraping the blackbox-exporter on port 9115 and Grafana is securely connected to your Telegram bot webhook.
​    Managed and maintained by an aspiring Cloud & DevOps Engineer. Feel free to reach out or fork this repository!
