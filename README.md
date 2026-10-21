# CodeArena ⚔️
> **Scalable Coding Assessment & Online Judge Platform**  
> *In Active Development*

CodeArena is a high-concurrency coding assessment and evaluation platform designed to automate programming challenges, real-time code execution, hidden test case verification, and submission metrics at scale.

---

## 🏗️ Architecture Overview

```mermaid
graph TD
    Client[Web Client / Monaco Editor] -->|HTTPS / WebSocket| API[API Gateway / Node.js & Express]
    API -->|Persist Metadata| DB[(PostgreSQL)]
    API -->|Push Submission Job| Queue[(Redis BullMQ)]
    WorkerPool[Worker Pool / Evaluator Service] -->|Pop Job| Queue
    WorkerPool -->|Spawn Sandbox| Sandbox[Docker / Isolated Container Sandbox]
    Sandbox -->|Execute & Trace| Runner[Language Execution Engine (C++, Python, Java, JS)]
    Runner -->|Verdict / Time / Memory| Sandbox
    Sandbox -->|Results| WorkerPool
    WorkerPool -->|Store Verdict| DB
    WorkerPool -->|Notify Verdict| API
    API -->|Real-time Verdict| Client
```

---

## ✨ Key Features

- **Interactive Code Editor:** Multi-language web-based editor powered by Monaco Editor with syntax highlighting, auto-completion, and customizable themes.
- **Asynchronous Execution Pipeline:** Distributed job queue with Redis-backed workers, isolating heavy compilation and runtime workloads from the primary API server.
- **Secure Sandboxed Code Execution:** Docker-isolated containers with strict cgroup limits (CPU time, memory caps) and restricted network access to prevent malicious code execution.
- **Automated Verification & Verdicts:** Exact match, floating-point tolerance, and regex-based output validation against hidden test cases.
- **Telemetry & Benchmarks:** Sub-millisecond tracking for execution latency, peak memory consumption, and runtime verdicts (AC, WA, TLE, MLE, CE, RE).
- **Code Similarity Review (Roadmap):** Token-based AST comparison for plagiarism detection across candidate submissions.

---

## 🛠️ Planned Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React.js, TypeScript, Monaco Editor, Tailwind CSS |
| **Backend & APIs** | Node.js, Express.js, TypeScript, REST APIs, WebSockets |
| **Queue & Cache** | Redis (BullMQ) |
| **Database** | PostgreSQL |
| **Execution Sandboxes** | Docker, Linux cgroups, C++ runtime wrappers |
| **DevOps & CI/CD** | Docker Compose, GitHub Actions |

---

## 🗺️ Roadmap & Milestones

- [x] Initial repository setup and system architecture design
- [ ] **Phase 1:** Core REST API, problem schemas, and database migrations (PostgreSQL)
- [ ] **Phase 2:** Isolated sandbox execution engine with container resource limits
- [ ] **Phase 3:** Redis worker pool integration for async submission processing
- [ ] **Phase 4:** Frontend UI with Monaco editor and live submission status via WebSockets
- [ ] **Phase 5:** Anti-plagiarism AST similarity pipeline and benchmark reporting

---

## 📄 License
MIT License. Created by [Saurabh Tiwari](https://github.com/SaurabhCodes-16).
