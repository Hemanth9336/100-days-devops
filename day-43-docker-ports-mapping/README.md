---

# 🐳 Day 43: Docker Port Mapping

## 🧠 Problem Statement

The Nautilus DevOps team needs to deploy an **Nginx container** on **Application Server 2 (`stapp02`)** and expose it to external users using port mapping.

---

## 📋 Requirements

* Pull Docker image: `nginx:alpine`
* Create a container named `news`
* Map **host port `6200` → container port `80`**
* Ensure the container remains **running**

---

## 🎯 Objective

* Deploy an Nginx container
* Configure port mapping
* Verify external access

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash id="r7k2mp"
ssh steve@stapp02
```

---

### 2️⃣ Switch to Root User

```bash id="x5n9qa"
sudo su -
```

---

### 3️⃣ Verify Docker Service

```bash id="p4c8wd"
systemctl status docker
```

Ensure it shows:

```id="z1k3vf"
active (running)
```

---

### 4️⃣ Pull Nginx Alpine Image

```bash id="t8v2lm"
docker pull nginx:alpine
```

---

### 5️⃣ Run Container with Port Mapping

```bash id="n6q4ys"
docker run -d \
--name news \
-p 6200:80 \
nginx:alpine
```

---

### 6️⃣ Verify Running Container

```bash id="c3m7az"
docker ps
```

Expected output should include:

```id="y2v8rl"
news   Up ...   0.0.0.0:6200->80/tcp
```

---

## 🧪 Verification

Test access from server:

```bash id="v1k9qp"
curl http://localhost:6200
```

---

## 🏁 Final Outcome

* Nginx container `news` successfully created
* Port mapping configured (`6200 → 80`)
* Container running and accessible

---

## 🔍 Key Concepts

| Concept        | Description                          |
| -------------- | ------------------------------------ |
| Port Mapping   | Connects host port to container port |
| `-p` flag      | Used to expose container ports       |
| Nginx          | Lightweight web server               |
| Container Port | Internal port (80)                   |
| Host Port      | External access port (6200)          |

---

## 💡 Key Learnings

* Exposing container services to host
* Understanding port mapping in Docker
* Running containers in detached mode
* Verifying container accessibility
* Real-world deployment setup

---

## 🔁 Workflow

```bash id="k5z2jw"
pull image → run container with -p → verify → access
```

---

## 🚀 Summary

Deployed an Nginx container with port mapping — enabling external access to containerized applications, a core concept in real-world DevOps and microservices architectures.

---
