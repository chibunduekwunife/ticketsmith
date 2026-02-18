
# TicketForge: Tight MVP you can actually ship

## Project Description

TicketForge is a web app for support ticket triage and response. Users can upload tickets (CSV or form), run an async triage pipeline, retrieve relevant KB articles, generate suggested replies with citations, and run QA checks before sending. The app demonstrates a real-world, event-driven workflow with audit trails and analytics.

## Setup Steps

1. **Clone the repo:**
	 ```bash
	 git clone <your-repo-url>
	 cd ticketsmith/ticket-smith
	 ```
2. **Install dependencies:**
	 ```bash
	 npm install
	 # or
	 yarn install
	 ```
3. **Set up the database:**
	 - Make sure you have [Docker](https://www.docker.com/) installed.
	 - Start PostgreSQL with Docker Compose:
		 ```bash
		 docker-compose up -d
		 ```
	 - Run Prisma migrations:
		 ```bash
		 npx prisma migrate dev --name init
		 ```
4. **Configure environment variables:**
	 - Copy `.env.example` to `.env` and fill in any required values (like `DATABASE_URL`).

## How to Run DB + App

1. **Start the database:**
	 ```bash
	 docker-compose up -d
	 ```
2. **Run the app:**
	 ```bash
	 npm run dev
	 # or
	 yarn dev
	 ```
3. **Visit:** [http://localhost:3000](http://localhost:3000)

## What the Project Demonstrates

- Event-driven ticket triage pipeline (async processing, retries, idempotency)
- Retrieval-Augmented Generation (RAG) with citation-only responses
- Automated QA guardrails for reply quality
- Evaluation harness with labelled tickets and metrics
- Structured logs/metrics and DLQ alerts

## Core Features (MVP)

1. Ticket ingest (CSV upload or simple form)
2. Auto-triage: category, priority, SLA risk
3. Searchable KB: add 10–30 help articles, retrieve top 3 relevant snippets
4. Suggested response with citations (only from KB)
5. Reply QA: checklist (steps, policy, links, tone)
6. Audit trail: store model suggestions and user edits

## What *not* to do in MVP

- Zendesk/Intercom integration
- Multi-tenant RBAC
- Sentiment analysis, duplicate detection, forecasting (all at once)
- Real-time dashboards/websockets

## Milestones

**Milestone 1:** Basic app + database (Day 1–3)
	- Tickets table + KB articles table
	- Create/list tickets
	- Upload CSV tickets

**Milestone 2:** Async pipeline (Day 4–6)
	- Enqueue job on ticket creation
	- Worker processes ticket, stores triage fields

**Milestone 3:** Retrieval + citations (Week 2)
	- Embedding + vector search for KB
	- Return top snippets, force citations

**Milestone 4:** QA guardrails (Week 2–3)
	- Response QA checks (rule-based + LLM judge)
	- Block/flag failed replies

**Milestone 5:** “Resume polish” features (Week 3–4)
	- Analytics page (categories, SLA risk, time-to-first-response)
	- Evaluation set and metrics

## Resume-Ready Bullets

- Built an event-driven ticket triage pipeline with async processing, retries, and idempotency.
- Implemented RAG with citation-only responses to reduce hallucinations and improve answer traceability.
- Added automated QA guardrails (policy checks + missing-step detection) to flag unsafe/low-quality replies.
- Created an evaluation harness with labelled tickets to measure triage accuracy and retrieval quality over time.
- Instrumented the system with structured logs/metrics and DLQ alerts for pipeline failures.

---

## Smaller Alternatives (Backup Projects)

**ClauseCraft:** Upload PDF → extract 6 fields → store → searchable list → renewal reminders. Skip risk scoring, redlines, and heavy workflows.

**FinOpsGuard:** Ingest a sample CUR-like CSV → detect anomalies → generate explanation + alert. Skip PR bot + org-wide IAM complexity.
