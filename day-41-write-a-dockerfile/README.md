---

# 🐳 Day 41: Write a Dockerfile

## 🧠 Problem Statement

The Nautilus DevOps team needs to create a **custom Docker image** for application testing on **Application Server 3 (`stapp03`)**.

A Dockerfile must be created at

```bash id="p3k9x1"
/opt/docker/Dockerfile
```

---

## 📋 Requirements

* Use base image: `ubuntu:24.04`
* Install `apache2`
* Configure Apache to run on port `6200`
* Do **not** modify other Apache configurations (like document root)

---

## 🎯 Objective

* Create a Dockerfile
* Install and configure Apache inside image
* Ensure Apache runs on required port

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash id="x8m4zp"
ssh banner@stapp03
```

---

### 2️⃣ Switch to Root User

```bash id="n6q2rl"
sudo su -
```

---

### 3️⃣ Create Directory for Dockerfile

```bash id="v5c1ta"
mkdir -p /opt/docker
cd /opt/docker
```

---

### 4️⃣ Create Dockerfile

```bash id="z2y8kd"
vi Dockerfile
```

---

### 5️⃣ Add Dockerfile Content

```dockerfile
FROM ubuntu:24.04

RUN apt update && \
    apt install -y apache2 && \
    sed -i 's/80/6200/g' /etc/apache2/ports.conf && \
    sed -i 's/:80/:6200/g' /etc/apache2/sites-available/000-default.conf

EXPOSE 6200

CMD ["apachectl", "-D", "FOREGROUND"]
```

---

## 🧪 Build the Image (Optional Verification)

```bash id="c9v7px"
docker build -t custom-apache:latest .
```

---

## 🧪 Run the Container (Optional)

```bash id="k4r2mw"
docker run -d -p 6200:6200 custom-apache:latest
```

---

## 🏁 Final Outcome

* Dockerfile created at `/opt/docker/Dockerfile`
* Apache configured to run on port `6200`
* Image ready to be built and used

---

## 🔍 Key Concepts

| Concept    | Description                         |
| ---------- | ----------------------------------- |
| Dockerfile | Script to build Docker images       |
| Base Image | Starting point (`ubuntu:24.04`)     |
| RUN        | Executes commands during build      |
| EXPOSE     | Defines container port              |
| CMD        | Default command when container runs |

---

## 💡 Key Learnings

* Writing custom Dockerfiles
* Installing packages during image build
* Configuring services inside images
* Managing ports in containerized apps
* Creating reusable container images

---

## 🔁 Workflow

```bash id="j7w3qn"
Dockerfile → build image → run container → verify
```

---

## 🚀 Summary

Created a custom Dockerfile to build an Apache-based image running on a non-default port — a key step toward building production-ready, reusable container images.

---
