# ⚡ AI-Powered SCADA Alarm Assistant

> An AI-powered Retrieval-Augmented Generation (RAG) application that helps SCADA engineers analyze industrial alarm logs, identify probable root causes, and generate incident reports using Spring AI and Large Language Models.

![Java](https://img.shields.io/badge/Java-21-red)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5-green)
![Spring AI](https://img.shields.io/badge/Spring-AI-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-pgvector-blue)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![License](https://img.shields.io/badge/License-MIT-green)

---

# 📌 Overview

Industrial SCADA systems continuously generate thousands of alarms from substations, transformers, sensors, PLCs, RTUs, and communication devices.

Engineers often spend valuable time manually reading alarm logs to determine:

* What happened?
* Why did it happen?
* What is the probable root cause?
* What actions should be taken?

This project demonstrates how **Generative AI** and **Retrieval-Augmented Generation (RAG)** can automate alarm analysis while ensuring responses are grounded in uploaded engineering documents instead of relying only on the LLM's general knowledge.

---

# 🎯 Problem Statement

Traditional SCADA systems provide alarm notifications but usually do not explain:

* Root cause
* Sequence of events
* Recommended actions
* Incident summaries

Engineers must manually investigate hundreds or thousands of alarms.

This project reduces investigation time by allowing engineers to upload alarm logs and ask questions in natural language.

Example:

**Question**

```
Why did Breaker-01 trip yesterday?
```

**AI Response**

```
Breaker-01 tripped after transformer temperature exceeded
95°C, causing voltage instability and protection relay activation.

Probable Root Cause:
Transformer Overheating

Recommended Action:
Inspect transformer cooling system and load distribution.
```

---

# 🚀 Features

## Alarm Log Upload

Supports:

* CSV
* TXT
* PDF

---

## Automatic Document Processing

Uploaded documents are automatically:

* Parsed
* Split into chunks
* Embedded using an AI embedding model
* Stored inside PostgreSQL using pgvector

---

## AI Chat Assistant

Ask engineering questions such as:

```
Why did breaker trip?

What happened yesterday?

Which transformer generated the highest alarms?

Summarize today's incidents.

What was the root cause?

Suggest corrective actions.
```

---

## Incident Report Generator

Automatically generates:

* Incident Summary
* Timeline
* Root Cause Analysis
* Recommended Actions

---

## Vector Search (RAG)

Instead of sending the complete document to the LLM,

the system:

* Creates embeddings
* Retrieves relevant chunks
* Sends only related context

Result:

* Faster
* More accurate
* Lower AI cost
* Reduced hallucinations

---

# 🏗️ Architecture

```
                 Upload Alarm Log
                         │
                         ▼
                File Processing
                         │
                         ▼
                  Chunk Documents
                         │
                         ▼
               Generate Embeddings
                         │
                         ▼
             PostgreSQL + pgvector
                         │
                         ▼
                  User Question
                         │
                         ▼
              Similarity Search
                         │
                         ▼
                 Relevant Chunks
                         │
                         ▼
                 Spring AI Prompt
                         │
                         ▼
                  OpenAI / Gemini
                         │
                         ▼
                 AI Generated Answer
```

---

# 🛠 Technology Stack

## Backend

* Java 21
* Spring Boot 3.5
* Spring AI
* Spring Security
* Spring Data JPA
* Maven

## AI

* OpenAI API / Gemini API
* Embedding Models
* Retrieval-Augmented Generation (RAG)

## Database

* PostgreSQL
* pgvector

## Documentation

* Swagger / OpenAPI

## Authentication

* JWT

## Deployment

* Docker
* Docker Compose

---

# 📂 Project Structure

```
src/main/java

controller/
service/
repository/
entity/
dto/
config/
rag/
security/
exception/
util/
```

---

# 📦 REST APIs

## Upload Alarm File

```
POST /api/upload
```

---

## AI Chat

```
POST /api/chat
```

Request

```json
{
  "question": "Why did breaker trip?"
}
```

Response

```json
{
  "answer": "Breaker tripped after transformer temperature exceeded safe limits."
}
```

---

## Generate Incident Report

```
POST /api/report
```

---

## List Uploaded Documents

```
GET /api/documents
```

---

# 🗄 Database Schema

## Document

| Field      | Type      |
| ---------- | --------- |
| id         | Long      |
| filename   | String    |
| uploadTime | Timestamp |

---

## DocumentChunk

| Field      | Type   |
| ---------- | ------ |
| id         | Long   |
| content    | Text   |
| embedding  | Vector |
| documentId | Long   |

---

## User

| Field    | Type             |
| -------- | ---------------- |
| id       | Long             |
| username | String           |
| password | String           |
| role     | ADMIN / ENGINEER |

---

# 🔒 Security

JWT Authentication

Supported Roles

* ADMIN
* ENGINEER

---

# 📖 Swagger

```
http://localhost:8080/swagger-ui.html
```

---

# 🐳 Docker

Containers

* Spring Boot
* PostgreSQL
* pgvector

Run

```bash
docker compose up --build
```

---

# 📁 Sample Alarm Log

```csv
Timestamp,Alarm

10:01,Transformer Temperature High

10:02,Voltage Drop

10:05,Breaker Trip

10:06,Communication Failure

10:08,Transformer Overload
```

---

# 💬 Example Conversation

**Question**

```
Why did breaker trip?
```

**Answer**

```
The uploaded alarm logs indicate that transformer temperature
crossed the configured threshold, resulting in a voltage drop.
The protection relay subsequently activated the breaker.

Probable Root Cause:
Transformer Overheating
```

---

# 📄 Incident Report

```
Incident Summary

Transformer experienced overheating.

Voltage instability detected.

Breaker protection activated.

Communication loss occurred after trip.

Root Cause

Transformer overload leading to excessive temperature.

Recommended Actions

Inspect transformer cooling system.

Verify relay settings.

Perform thermal inspection.

Balance electrical load.
```

---

# 🎯 Interview Demonstration

### Step 1

Start the application.

---

### Step 2

Open Swagger.

---

### Step 3

Upload

```
sample-alarm.csv
```

---

### Step 4

Ask

```
Why did breaker trip?
```

---

### Step 5

Ask

```
What was the root cause?
```

---

### Step 6

Generate Incident Report.

---

### Step 7

Explain the RAG workflow:

1. Upload document
2. Split into chunks
3. Generate embeddings
4. Store vectors
5. Retrieve similar chunks
6. Build prompt
7. AI generates a grounded response

---

# 🌟 Key Learning Outcomes

This project demonstrates practical experience with:

* Enterprise Java Development
* Spring Boot REST APIs
* Spring AI
* Retrieval-Augmented Generation (RAG)
* Vector Databases
* PostgreSQL + pgvector
* AI Prompt Engineering
* File Processing
* JWT Authentication
* Swagger Documentation
* Docker Deployment
* Clean Architecture
* Industrial Automation Software Concepts

---

# 🚀 Future Enhancements

* Live SCADA gateway integration
* MQTT alarm streaming
* OPC UA connectivity
* Kafka event processing
* Multi-document semantic search
* Alarm severity prediction
* Predictive maintenance using AI
* Real-time dashboard with WebSockets
* Multi-tenant support
* Audit logging and analytics

---

# 👨‍💻 Author

**Ayush Pallav Pandey**

Built as a portfolio project to demonstrate modern AI-powered industrial software development using Java, Spring Boot, Spring AI, PostgreSQL, and Retrieval-Augmented Generation (RAG).
