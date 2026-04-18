# 🚀 Student Record App – Dockerized CI/CD Setup

## 📌 Overview

This project is a full-stack CRUD application for managing student records.

It has been enhanced with:

* Docker containerization (frontend + backend + database)
* Docker Compose for multi-container orchestration
* GitHub Actions CI pipeline to automatically build and push images

---
## 🔁 Getting Started (Fork, Clone, and Setup)

### 1. Fork the Repository

Click the **Fork** button on the top right of the original repository to create your own copy.

repo
https://github.com/Simran-210803/STUDENT-RECORD-API

---

### 2. Clone Your Fork

```bash
git clone https://github.com/Adaobilynda1234/STUDENT-RECORD-API.git
cd STUDENT-RECORD-API
```

---

### 3. Create a New Branch

It is best practice to work on a separate branch:

```bash
git checkout -b feature/docker-setup
```

---

### 4. Make Your Changes

Add:

* Dockerfiles (frontend & backend)
* docker-compose.yml
* GitHub Actions workflow
* README updates

---

### 5. Commit and Push

```bash
git add .
git commit -m "Add Docker setup and CI pipeline"
git push origin feature/docker-setup
```

---

### 6. Merge into Main Branch

To trigger the CI pipeline:

```bash
git checkout main
git merge feature/docker-setup
git push origin main
```

---

### ⚠️ Important

The CI pipeline is configured to run only on the `main` branch, so make sure your final changes are merged into `main`.


## 🧱 Tech Stack

* **Frontend**: React (Create React App)
* **Backend**: Node.js, Express
* **Database**: MongoDB
* **Containerization**: Docker, Docker Compose
* **CI/CD**: GitHub Actions
* **Web Server (Frontend)**: Nginx

---

## 📂 Project Structure

```
STUDENT-RECORD-API/
├── backend/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── src/
├── frontend/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── src/
├── docker-compose.yml
├── .github/
│   └── workflows/
│       └── docker-build.yml
└── README.md
```

---

## 🐳 Dockerization

### 🔹 Backend Dockerfile

**File:** `backend/Dockerfile`

**Steps:**

1. Use lightweight Node.js image (`node:18-alpine`)
2. Set working directory
3. Copy dependency files
4. Install dependencies using `npm install`
5. Copy source code
6. Expose port `5000`
7. Start server

---

### 🔹 Frontend Dockerfile

**File:** `frontend/Dockerfile`

Uses a **multi-stage build**:

#### Stage 1: Build React App

* Install dependencies
* Run `npm run build`

#### Stage 2: Serve with Nginx

* Copy build files into Nginx
* Serve static files on port `80`

---

## ❓ Why Use Nginx for React?

React’s `npm start` is only for development.

In production:

* React builds static files (`HTML, CSS, JS`)
* These files need a web server

**Nginx is used because:**

* It is fast and lightweight
* It efficiently serves static files
* It is the industry standard for frontend deployment

---



## 🧩 Docker Compose Setup

**File:** `docker-compose.yml`

### Services:

### 1. Backend

* Builds from `./backend`
* Runs on port `5000`
* Connects to MongoDB

### 2. Frontend

* Builds from `./frontend`
* Runs on port `3000`
* Depends on backend

### 3. MongoDB

* Uses official `mongo` image
* Stores data using Docker volumes

---

### ⚠️ Important Note

Inside Docker:

```
mongodb://mongo:27017/studentdb
```

* `mongo` = service name (NOT localhost)
* Containers communicate via service names

---

## ▶️ Running the App Locally

```bash
docker compose up --build
```

Access:

* Frontend → http://localhost:3000
* Backend → http://localhost:5000

---

## 🔁 CI/CD Pipeline (GitHub Actions)

**File:** `.github/workflows/docker-build.yml`

### Trigger:

* Runs on every push to `main`

---

### 🔹 Pipeline Steps

1. **Checkout Code**

   * Pulls repository into runner

2. **Install Dependencies**

   * Backend → `npm install`
   * Frontend → `npm install`

3. **Run Test/Lint**

   * Runs `npm test`
   * Does not fail if no tests exist

4. **Setup Docker Buildx**

   * Enables advanced Docker builds

5. **Login to Docker Hub**

   * Uses GitHub secrets:

     * `DOCKERHUB_USERNAME`
     * `DOCKERHUB_TOKEN`

6. **Build & Push Backend Image**

   * Tags:

     * `latest`
     * commit SHA

7. **Build & Push Frontend Image**

   * Tags:

     * `latest`
     * commit SHA

---

## 🏷️ Docker Image Tagging Strategy

Each image is tagged with:

* **latest**

  * Always points to the most recent build

* **commit SHA**

  * Unique identifier for each version

### Example:

```
student-record-backend:latest
student-record-backend:abc1234
```

---

### 🎯 Benefits

* Track deployments easily
* Rollback to previous versions
* Maintain version history.

---

## 🔐 GitHub Secrets Required

Set in repository settings:

* `DOCKERHUB_USERNAME`
* `DOCKERHUB_TOKEN`

---

## 📸 Submission Requirement

Include:

* Screenshot of successful GitHub Actions run
* Screenshot of images in Docker Hub

---

## ✅ Summary of Work Done

* Created Dockerfiles for frontend and backend
* Used Nginx for production-ready frontend serving
* Used `npm install` for dependency installation
* Configured Docker Compose with MongoDB
* Built CI pipeline for automated image build and push
* Implemented tagging strategy (`latest` + commit SHA)

---

## 🧠 Key Learning Points

* Multi-container applications with Docker
* CI/CD automation with GitHub Actions
* Production vs development environments
* Container networking (service names vs localhost)
* Image versioning strategies

---

## 🏁 Conclusion

This project demonstrates a complete workflow from development to deployment using modern DevOps practices, including containerization and continuous integration.

---
