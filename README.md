# ProjFlix 🎬
An end-to-end streaming platform inspired by Netflix.

**Highlights (for recruiters):**
- **C++ backend module** including a **multithreaded TCP server**, synchronization, and recommendation logic
- Full-stack integration with **Node.js/Express + MongoDB**, **React** web client, and **Android (Java)** app
- Docker-based setup for a reproducible local environment

---

## Tech Stack
- **Backend / Services:** C++ (multithreading, mutex/condition_variable), Node.js, Express
- **Database:** MongoDB
- **Clients:** React (Web), Android (Java)
- **Infra:** Docker, Docker Compose

---

## Repository Structure
- `recommend/` – C++ recommendation + multithreaded server (Thread Pool / Thread-per-client implementations)
- `api/` – Node.js/Express API + MongoDB integration
- `netflix/` – React web client
- `Netflix android/` – Android client (Java)
- `wiki/` – Additional documentation (web + android)
- `samples/` – Setup screenshots and configuration examples

---

## Main Features
- User & content management (via API)
- Web UI (React) + Android app
- Recommendation component implemented in **C++**
- Multithreaded server handling concurrent requests

---

## Quick Start (Docker)
### Prerequisites
- Docker + Docker Compose

### Run
```bash
docker compose up --build
