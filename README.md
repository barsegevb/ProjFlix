# ProjFlix 🎬
An end-to-end streaming platform **inspired by Netflix** (academic project).

**What you’ll find here (quick highlights):**
- **C++ recommendation service** with a **multithreaded TCP server** (thread pool + synchronization)
- **Node.js/Express REST API** backed by **MongoDB**
- **React** web client + **Android (Java)** mobile client
- **Docker Compose** setup for running the system locally

---

## Table of Contents
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Repository Structure](#repository-structure)
- [Quick Start (Docker)](#quick-start-docker)
- [Environment Variables](#environment-variables)
- [Run Web / API Without Docker (Optional)](#run-web--api-without-docker-optional)
- [Android App Setup](#android-app-setup)
- [Documentation](#documentation)
- [Troubleshooting](#troubleshooting)

---

## Architecture
High level flow:

1. **Clients** (React Web / Android) call the **REST API** (Node.js/Express).
2. The API reads/writes data in **MongoDB**.
3. For recommendations and “watch” updates, the API communicates with the **C++ recommender** over **TCP**.

---

## Tech Stack
- **C++**: multithreaded TCP server, thread pool, synchronization (mutex / condition_variable)
- **Backend**: Node.js, Express
- **Database**: MongoDB
- **Web**: React
- **Mobile**: Android (Java)
- **Infra**: Docker, Docker Compose

---

## Repository Structure
- `recommend/` – **C++** recommender + multithreaded server
- `api/` – **Node.js/Express** API + MongoDB integration (also connects to the C++ recommender)
- `netflix/` – React web client
- `Netflix android/` – Android client (Java)
- `wiki/` – usage + setup notes for web and android
- `samples/` – screenshots / configuration examples

---

## Quick Start (Docker)

### Prerequisites
- Docker + Docker Compose

### 1) Create a `.env` file (recommended)
Create a file named **`.env`** in the repository root (same folder as `docker-compose.yml`).

Example:
```env
# MongoDB connection string (your DB name/user/pass as needed)
CONNECTION_STRING=mongodb://mongo:27017/projflix

# API
CONTAINER_PORT=3000
JWT_SECRET=change_me_to_a_long_random_secret

# Recommender service (C++)
RECOMMENDATION_PORT=5555

# React web client -> API base URL (from the browser)
REACT_APP_API_URL=http://localhost:3000
```

### 2) Run
```bash
docker compose up --build
```

### 3) Open
- **Web client:** http://localhost:3000 (if your React container maps 3000)
- **API:** http://localhost:<API_PORT> (depends on your compose mapping)

> Note: port mappings are defined in `docker-compose.yml`.  
> If you changed ports in `.env`, make sure the compose file maps them accordingly.

---

## Environment Variables
The API and services rely on these environment variables:

- `CONNECTION_STRING` – MongoDB connection string
- `JWT_SECRET` – JWT signing secret
- `PORT` / `CONTAINER_PORT` – API port (depending on how you run it)
- `RECOMMENDATION_IP` – hostname/IP of the C++ recommender (Docker service name is usually `recommender_server`)
- `RECOMMENDATION_PORT` – TCP port exposed by the C++ recommender
- `REACT_APP_API_URL` – base URL used by the React app to reach the API

---

## Run Web / API Without Docker (Optional)

### API (Node.js)
```bash
cd api
npm install
npm start
```

### Web (React)
```bash
cd netflix
npm install
npm start
```

### C++ recommender (CMake)
```bash
cd recommend
mkdir -p build
cd build
cmake ..
make
./myapp <PORT>
```

---

## Android App Setup
1. Start the backend services (Docker recommended).
2. Open `Netflix android/` in Android Studio.
3. Update the Android configuration to point to your API host:
   - If running on an **Android emulator**: `http://10.0.2.2:<API_PORT>`
   - If running on a **physical device**: `http://<YOUR_PC_LOCAL_IP>:<API_PORT>`
4. See `wiki/android.md` and `samples/` for configuration screenshots and file locations.

---

## Documentation
More detailed explanations (screenshots, configuration, features) are available under:
- `wiki/web.md`
- `wiki/android.md`

---

## Troubleshooting
- **Web/Android can’t reach the API**: verify the base URL (`REACT_APP_API_URL` / Android config) and exposed ports.
- **Android + localhost**: on emulator use `10.0.2.2`, on real device use your PC’s local IP.
- **Recommendations not working**: ensure `RECOMMENDATION_IP` and `RECOMMENDATION_PORT` match the running C++ service.

---

## LinkedIn / Portfolio one-liner (optional)
> GitHub repository containing the **C++ multithreaded backend service**, recommendation logic, and the full project setup.
