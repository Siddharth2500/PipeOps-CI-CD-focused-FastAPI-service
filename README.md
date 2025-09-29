# 🚀 PipeOps — CI/CD & DevOps Microservice

![Python](https://img.shields.io/badge/Python-3.11-blue.svg?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688?logo=fastapi)
![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Ready-326CE5?logo=kubernetes&logoColor=white)
![CI/CD](https://img.shields.io/badge/GitHub_Actions-CI/CD-2088FF?logo=github-actions&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-E6522C?logo=prometheus)

---

## 📖 Overview

**PipeOps** is a real-world **DevOps & Cloud Engineering demo project** built in **Python** using **FastAPI**.  
It demonstrates how to design, containerize, test, monitor, and deploy a microservice that simulates **CI/CD pipelines**.

Key Features:
- ✅ **Health & Readiness probes** for container orchestration  
- 📊 **Prometheus metrics** (request count & latency histograms)  
- 🧪 **Unit tests** with `pytest`  
- 🐳 **Dockerfile** for container builds  
- ⚡ **GitHub Actions** workflow for CI/CD automation  
- ☸️ **Kubernetes manifests** (Deployment, Service)  
- 🔧 **Makefile** for developer shortcuts  

---

## 🛠️ Tech Stack

| Layer                | Tool/Language         | Why we use it |
|----------------------|----------------------|---------------|
| **Programming**      | ![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python) | Widely used in DevOps scripting & APIs |
| **Framework**        | ![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white) | Lightweight, async, auto-docs |
| **Containerization** | ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) | Package & run consistently |
| **Orchestration**    | ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes) | Scaling, probes, deployment |
| **Monitoring**       | ![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus) | Metrics scraping |
| **CI/CD**            | ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=github-actions) | Automated tests & build pipeline |

---

## 🌐 Architecture

<p align="center">
  <img src="https://raw.githubusercontent.com/Siddharth2500/pipeops-assets/main/architecture.png" alt="PipeOps Architecture" width="600"/>
</p>

1. **User** hits API endpoints (`/health`, `/ready`, `/pipeline/run`)  
2. **FastAPI app** processes request, updates **Prometheus metrics**  
3. Logs and metrics are collected for observability  
4. Deployed as a **Docker container** → **Kubernetes Deployment & Service**  
5. **GitHub Actions** ensures CI/CD automation  

---

## 📦 Repository Structure

```bash
pipeops/
├── app/
│   └── main.py         # FastAPI app
├── tests/
│   └── test_health.py  # Unit tests
├── Dockerfile          # Container build
├── requirements.txt    # Dependencies
├── Makefile            # Dev shortcuts
├── k8s/
│   ├── deployment.yaml # Kubernetes deployment
│   └── service.yaml    # Kubernetes service
└── README.md
▶️ Running in Google Colab
This repo is designed to run in Google Colab for quick experiments.

python
Copy code
!git clone https://github.com/Siddharth2500/pipeops.git
%cd pipeops
!pip install -r requirements.txt

!uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
Then test endpoints inside Colab:

python
Copy code
import httpx
print(httpx.get("http://127.0.0.1:8000/health").json())
print(httpx.get("http://127.0.0.1:8000/ready").json())
🔗 API Endpoints
Method	Path	Description
GET	/	Service info
GET	/health	Health check (liveness)
GET	/ready	Readiness check
GET	/metrics	Prometheus metrics (requests/latency)
POST	/pipeline/run	Simulates CI/CD pipeline execution

Example request:

bash
Copy code
curl -X POST http://localhost:8080/pipeline/run \
  -H "Content-Type: application/json" \
  -d '{"repo":"github.com/Siddharth2500/sample","branch":"main"}'
Response:

json
Copy code
{
  "repo": "github.com/Siddharth2500/sample",
  "branch": "main",
  "steps": ["pytest", "docker build && docker push"],
  "status": "queued"
}
🧪 Testing
Run all tests:

bash
Copy code
pytest -q
Example test (tests/test_health.py):

python
Copy code
def test_health():
    res = client.get("/health")
    assert res.status_code == 200
    assert res.json() == {"status": "ok"}
🐳 Docker Usage
Build the image:

bash
Copy code
docker build -t pipeops:latest .
Run container:

bash
Copy code
docker run -p 8080:8080 pipeops:latest
Visit http://localhost:8080/health.

☸️ Kubernetes Deployment
k8s/deployment.yaml & k8s/service.yaml included.

Deploy:

bash
Copy code
kubectl apply -f k8s/
kubectl get pods
kubectl port-forward svc/pipeops 8080:80
Check health:

bash
Copy code
curl http://localhost:8080/health
📊 Metrics & Monitoring
Prometheus endpoint: /metrics

Example metrics:

pgsql
Copy code
# HELP http_requests_total Total HTTP requests
http_requests_total{method="GET",path="/health",status="200"} 5.0
# HELP http_request_duration_seconds HTTP request latency seconds
http_request_duration_seconds_bucket{method="GET",path="/",le="0.1"} 2.0
Visualize with Grafana dashboards

🧑‍💻 CI/CD Pipeline
GitHub Actions workflow (.github/workflows/ci.yml):

Checkout code

Install dependencies

Run tests

On main: build & push Docker image to GitHub Container Registry

🎯 Roadmap
 Add authentication (JWT/API key)

 Add logging with correlation IDs

 Expand /pipeline/run to trigger real workflows (GitHub Actions, Argo, Tekton)

 Helm charts for easier Kubernetes deployment

 Add tracing with OpenTelemetry

📸 Screenshots
<p align="center"> <img src="https://raw.githubusercontent.com/Siddharth2500/pipeops-assets/main/fastapi-docs.png" alt="FastAPI Docs" width="700"/> </p>
Swagger UI auto-docs available at /docs

ReDoc docs at /redoc

📧 Contact
Author: Siddharth Raut

Role: Cloud & DevOps Engineer

Email: siduk2500@gmail.com

LinkedIn: linkedin.com/in/siddharth-raut-

📝 License
MIT License © 2025 Siddharth Raut

markdown
Copy code
