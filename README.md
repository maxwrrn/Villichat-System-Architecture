# Villichat | Enterprise AI Customer Support Platform


**Villichat** is a containerized AI-SaaS platform that automates customer support workflows for **30+ enterprise clients**. It integrates secure LLM orchestration with a proprietary lead-generation engine (**Schematica**) to drive conversion and engagement.

---

## 🚀 Key Features

* **Autonomous Agent Orchestration:** Utilizes custom-tuned LLMs (OpenAI) to handle complex customer queries with 95% resolution accuracy.
* **Zero-Config Integration:** Clients embed a lightweight JavaScript widget (`villichat-widget.js`) to instantly deploy the AI.
* **Hybrid Intelligence Engine:** Powered by **Schematica** (Internal Service) for real-time lead qualification and business metadata analysis.
* **Multi-Tenant Architecture:** Secure data isolation for all 30+ business clients using Role-Based Access Control (RBAC).

## 🛠 System Architecture

The platform follows a **Microservices-ready** architecture, deployed via Docker containers on Railway.

### Core Stack
* **Backend:** Python (Flask/Gunicorn)
* **Infrastructure:** Docker, Nginx (Reverse Proxy)
* **Database:** PostgreSQL (Client Data), Redis (Conversation Caching)
* **AI Layer:** OpenAI API (Context-Aware Embeddings)

### Data Flow
1.  **Widget:** User sends message via `villichat-widget.js`.
2.  **API Gateway:** Flask receives payload & authenticates origin.
3.  **Context Retrieval:** System fetches business-specific knowledge base (RAG).
4.  **LLM Inference:** Model generates response based on retrieved context.
5.  **Action:** Lead data is parsed and sent to the client dashboard.

---

## 📦 Deployment (DevOps)

Villichat utilizes a CI/CD pipeline for zero-downtime deployments.

```dockerfile
# Production Dockerfile Structure
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
