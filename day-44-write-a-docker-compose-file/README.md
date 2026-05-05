---

# 🐳 Day 44: Write a Docker Compose File

## 🧠 Problem Statement

The Nautilus DevOps team needs to deploy a **static website** using an **httpd container** on **Application Server 1 (`stapp01`)** using Docker Compose.

A Docker Compose file must be created at:

```bash
/opt/docker/docker-compose.yml
```

---

## 📋 Requirements

* Use image: `httpd:latest`
* Container name: `httpd`
* Map **host port `8089` → container port `80`**
* Mount volume:

  * Host: `/opt/dba`
  * Container: `/usr/local/apache2/htdocs`
* Do **not modify existing data** in mounted directories

---

## 🎯 Objective

* Create a Docker Compose file
* Deploy container using Compose
* Configure ports and volumes
* Verify container and website

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash
ssh tony@stapp01
```

---

### 2️⃣ Switch to Root User

```bash
sudo su -
```

---

### 3️⃣ Create Directory for Compose File

```bash
mkdir -p /opt/docker
cd /opt/docker
```

---

### 4️⃣ Create Docker Compose File

```bash
vi docker-compose.yml
```

---

### 5️⃣ Add Compose Configuration

```yaml
version: '3.8'

services:
  web:
    image: httpd:latest
    container_name: httpd
    ports:
      - "8089:80"
    volumes:
      - /opt/dba:/usr/local/apache2/htdocs
```

---

### 6️⃣ Start the Container

```bash
docker compose up -d
```

---

### 7️⃣ Verify Running Container

```bash
docker ps
```

Expected:

```bash
httpd   Up   0.0.0.0:8089->80/tcp
```

---

## 🧪 Verification

Test the website:

```bash
curl http://localhost:8089
```

---

## 🏁 Final Outcome

* Docker Compose file created successfully
* httpd container deployed
* Port mapping configured (`8089 → 80`)
* Volume mounted correctly
* Website accessible

---

## 🔍 Key Concepts

| Concept        | Description                                 |
| -------------- | ------------------------------------------- |
| Docker Compose | Tool to define multi-container applications |
| Service        | Container definition inside Compose         |
| Port Mapping   | Expose container ports to host              |
| Volume Mount   | Share data between host and container       |
| container_name | Custom name for container                   |

---

## 💡 Key Learnings

* Writing Docker Compose files
* Managing containers declaratively
* Configuring ports and volumes
* Deploying applications using Compose
* Simplifying container management

---

## 🔁 Workflow

```bash
write compose → docker compose up → verify → access
```

---

## 🚀 Summary

Deployed an Apache (httpd) container using Docker Compose with port mapping and volume mounting — a real-world approach to managing containerized applications efficiently.

---
