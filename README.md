<!-- README.md -->

<div align="center">

# Askpglog

**AI-powered PostgreSQL log analysis for fast root-cause detection**

</div>

---

## Overview

**Askpglog** is a specialized tool for PostgreSQL log analysis with a focus on root cause detection. Using semantic search, AI-driven insights, and vector embeddings stored in the **Qdrant** Vector Store, it identifies errors, warnings, slow queries, deadlocks, and unusual patterns across multiple log files. By providing contextual events and concise AI-generated summaries, Askpglog helps database engineers and developers quickly pinpoint the underlying causes of issues and take effective corrective actions.

---

## Qdrant Technology

**Qdrant** is an open-source vector database for fast and scalable semantic search. It stores and indexes high-dimensional vector embeddings, supports real-time updates, filtering, and similarity search, and is ideal for AI-powered search and recommendations.

---

## Key Features

### Log Upload & Ingestion
- Supports `.csv`, `.log`, `.txt`, `.pdf`, `.docx` log files  
- Automatically parses events and stores them in PostgreSQL

### Semantic Log Search
- Uses Qdrant vector embeddings for natural language queries  
- Finds similar log lines even if keywords don’t match exactly

### Adaptive Time Context
- Search results include surrounding events within a ± time window  
- Helps understand what happened before and after an error

### Deadlock Detection
- Detects deadlocks in logs  
- Shows the last executed SQL statement per PID to debug issues

### Severity Insights
- Groups logs by severity: **ERROR**, **WARNING**, **FATAL**, **INFO**  
- Quick filtering for high-priority issues

### AI Summaries & Fixes
- Summarizes root causes using LLMs (e.g., OpenAI API)  
- Suggests possible fixes or next steps

### Interactive UI
- Built with **Streamlit**  
- Upload logs, run queries, and visualize issues in a clean interface

---

## How It Works

1. User uploads PostgreSQL log files via the Streamlit interface  
2. Logs are parsed and stored in PostgreSQL  
3. Embeddings are generated and stored in Qdrant  
4. User enters a query or pastes a log message  
5. System retrieves matching logs + related context  
6. AI summarizes potential causes and fixes

---

## Typical Use Cases

- Root cause analysis of PostgreSQL errors and incidents  
- Debugging deadlocks in production systems  
- Investigating performance slowdowns  
- Quickly searching logs with natural language  
- Generating summaries for incident reports  
- Filtering noise and focusing on critical issues


## Setup (Docker Compose)

> **Prereqs**
> - Docker & Docker Compose v2 installed
> - Ports **8501** (app), **5433** (PostgreSQL on host), **6333** (Qdrant) are available
> - This repository already includes `docker-compose.yml` and a `.env` template

---

### 1) Configure `.env`

Fill in the sensitive values. **Do not commit real secrets**.

```bash
# PostgreSQL
PG_HOST=postgres
PG_USER=postgres
PG_PASSWORD=change_me                   # <-- REQUIRED (non-empty)
PG_DB=tsdb
PG_PORT=5432

# Qdrant
QDRANT_HOST=qdrant
QDRANT_PORT=6333
QDRANT_URL=http://qdrant:6333

# OpenAI (needed for AI summaries & fixes)
OPENAI_API_KEY=sk-******************************   # <-- REQUIRED for AI features

# Docker Hub (fixed for public image)
DOCKERHUB_USERNAME=askpglog
```

### 2) (Optional) Adjust data persistence

By default, the compose file persists data to these host paths:

PostgreSQL → /var/lib/docker-volumes/postgres

Qdrant → /var/lib/docker-volumes/qdrant

If you prefer different paths, edit the volumes: mappings in docker-compose.yml.
(Alternatively, switch to named volumes if you maintain your own compose variant.)

### 3) Start the stack

From the repo root:

# pull the published images
docker compose pull

# start all services in the background
docker compose up -d


This brings up:

app (Streamlit UI) on http://localhost:8501

postgres on host port 5433 (container 5432)

qdrant on http://localhost:6333


### 4) Verify everything is healthy
# Check containers & health status
docker ps

# Tail app logs
docker compose logs -f app

# Qdrant alive?
curl http://localhost:6333/collections

# PostgreSQL reachable?
PGPASSWORD="$PG_PASSWORD" psql -h localhost -p 5433 -U "$PG_USER" -d "$PG_DB" -c '\l'


Open the UI: http://localhost:8501
