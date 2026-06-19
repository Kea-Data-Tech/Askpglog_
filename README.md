# 🚀 AskPgLog

**AskPgLog** is an advanced PostgreSQL log analysis and intelligence platform designed for **root cause detection, performance optimization, and AI-driven database insights**.

It combines **semantic search (Qdrant)**, **LLM-based reasoning (OpenAI / Ollama)**, and **PostgreSQL analytics** to help engineers quickly debug issues, optimize queries, and understand database behavior at scale.

---

# 🚀 Key Features

## 📄 Log Upload & Ingestion
- Supports `.log` and `.txt` PostgreSQL log files
- Automatic parsing into structured events
- Stores processed logs in **PostgreSQL**
- Fully automated ingestion pipeline (no manual steps required)

---

## 🔍 Semantic Log Search (AI + Qdrant)
- Uses **Qdrant vector database**
- Natural language search across logs
- Finds similar patterns even without exact keywords
- Context-aware retrieval (± time window expansion)

---

## 🧠 AI-Powered Log Analysis
- Uses **LLMs (OpenAI / Ollama)**
- Generates:
  - Root cause analysis
  - Incident summaries
  - Suggested fixes
- Converts raw logs into actionable engineering insights

---

## 📊 Log Classification Engine
- Automatically classifies logs into:
  - ERROR
  - WARNING
  - FATAL
  - INFO
- Provides severity breakdown charts
- Helps prioritize production issues

---

## 🔁 Repeated Log Detection
- Detects duplicate / recurring logs
- Identifies systemic failures
- Helps detect noisy or looped errors

---

## ⚡ Slow Query Detection
- Extracts slow queries from PostgreSQL logs
- Requires query duration logging enabled
- Identifies performance bottlenecks in production

---

## ⚡ Query Optimization Engine (EXPLAIN ANALYZE)
- Runs PostgreSQL `EXPLAIN ANALYZE`
- Detects:
  - Sequential scans
  - Missing indexes
  - Expensive joins
  - High-cost query plans
- AI suggestions:
  - Index recommendations
  - Query rewrites
  - Performance tuning strategies

---

## 🧬 PostgreSQL Schema Embedding
- Extracts schema metadata:
  - Tables
  - Columns
  - Constraints
  - Indexes
- Stores embeddings in **Qdrant**
- Improves AI contextual understanding of database structure

---

## ⏱ Adaptive Time Context Engine
- Retrieves logs with surrounding time context
- Reconstructs full incident timelines
- Helps trace root causes across events

---

## 🧯 Deadlock Detection
- Detects PostgreSQL deadlocks
- Maps last executed queries per PID
- Helps debug transaction conflicts in production

---

## 📊 Severity Insights Dashboard
- Visual breakdown of log severity levels
- System health trends
- Incident triage dashboard

---

## 💬 Chat-Based Log Exploration
Ask questions like:
- “Why did this query fail?”
- “Show errors in last 10 minutes”
- “What caused the spike at 2 AM?”

AI responds with contextual explanations using logs + embeddings.

---

## 🕘 HISTORY TAB (IMPORTANT)
The **History Tab** stores all AI interactions:

### 📌 Features:
- Stores every AI-generated response
- Tracks user queries and system answers
- Maintains chronological analysis history
- Helps in:
  - Incident audits
  - Debugging past issues
  - Reviewing AI recommendations
  - Knowledge retention for teams

### 📌 Benefits:
- Prevents repeated debugging effort
- Provides traceability for production incidents
- Acts as an internal knowledge base
- Useful for DevOps / DBA audits

---

# ⚙️ How It Works

1. Upload PostgreSQL log files via Streamlit UI  
2. Logs are parsed and stored in PostgreSQL  
3. Embeddings generated using **sentence-transformers / Ollama**  
4. Stored in **Qdrant vector database**  
5. User queries processed using semantic + keyword search  
6. AI generates explanations, fixes, and insights  
7. All interactions stored in **History Tab**

---

# 🚀 App Workflow

## 1️⃣ Backend Setup
- Configure PostgreSQL connection
- Ensure **Qdrant + Ollama** are running
- Verify environment variables

---

## 2️⃣ Log Upload
- Upload `.log` or `.txt` files
- Automatic ingestion pipeline starts
- No manual processing required

---

## 3️⃣ Qdrant Validation
- Run smoke test for vector DB
- Ensure embeddings are stored correctly

---

## 4️⃣ Schema Embedding (Optional)
- Click **Embed PostgreSQL Schema**
- Enhances AI understanding of database structure

---

## 5️⃣ Analysis Features

### 🚀 Log Classification
- Categorizes logs into severity levels

### 🚀 Repeated Logs
- Detects duplicate patterns

### 🚀 AI Analysis
- Root cause + fixes generation

### 🚀 Slow Queries
- Identifies performance issues

### 🚀 Query Optimization
- Uses `EXPLAIN ANALYZE`
- Suggests performance improvements

---

## 6️⃣ Qdrant Management Tab
- Reset log collections
- Reset schema embeddings
- Reset cache collections (cost optimization)

---

## 7️⃣ PostgreSQL Reset (Optional)
- Clear analysis tables
- Reset system for fresh analysis

---

# 🧠 Core Technologies

- Streamlit (UI)
- PostgreSQL (logs + storage)
- Qdrant (vector database)
- Ollama (local LLM + embeddings)
- OpenAI API (AI reasoning)
- Docker (deployment)
- EXPLAIN ANALYZE (query tuning)

---

# 🚀 Use Cases

- PostgreSQL incident debugging
- Query performance optimization
- Production log monitoring
- Root cause analysis
- AI-powered DevOps assistant
- Performance tuning recommendations

---

# ⚠️ Prerequisites

- Docker installed
- Docker Compose v2
- PostgreSQL running in container
- OpenAI API key (optional but recommended)

---

# 📦 Deployment (Docker Compose)

## 📁 Project Structure Requirement
Make sure your repo contains:
docker-compose.yml
.env

## 1️⃣ Configure `.env`
```env
# PostgreSQL
PG_HOST=postgres
PG_USER=postgres
PG_PASSWORD=change_me
PG_DB=tsdb
PG_PORT=5432

# Qdrant
QDRANT_URL=http://qdrant:6333

# Ollama
OLLAMA_URL=http://ollama:11434

# Optional external DB
OG_DB=
OG_USER=postgres
OG_PASSWORD=
OG_HOST=

# Linux / Windows note:
# Windows/Mac → host.docker.internal
# Linux → 172.17.0.1

OG_PORT=

# Docker Hub
DOCKERHUB_USERNAME=askpglog
```

---
# After configuring .env

## 2️⃣ Start services
```docker compose pull```
```docker compose up -d```

## 3️⃣ Check Running Containers
```docker ps```

## 4️⃣ View Logs
```docker compose logs -f app```

## 🌐 Service URLs
🚀 App → http://localhost:8501
🔎 Qdrant → http://localhost:6333/collections
🐘 PostgreSQL → http://localhost:5433
🧠 Ollama → http://localhost:11434

## 🧯 Maintenance Commands
## 🌐 Stop system 
```docker compose down```

## 🌐 Remove volumes (reset all data)
```docker compose down -v```

## 🌐 Rebuild system
```docker compose build --no-cache```
```docker compose up -d```

## 🌐 Remove volumes (reset all data)
```docker compose down -v```

## 🌐 Rebuild system
```docker compose build --no-cache```
```docker compose up -d```













