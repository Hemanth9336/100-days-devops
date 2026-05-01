---

# 🐳 Day 40: Docker EXEC Operations

## 🧠 Problem Statement

A Nautilus DevOps team member left a task incomplete inside a running Docker container **`kkloud`** on **Application Server 1 (`stapp01`)**.

Your task is to complete the configuration inside the container.

---

## 📋 Requirements

* Install `apache2` inside the container
* Configure Apache to listen on port `8088` (instead of default `80`)
* Ensure Apache listens on all interfaces (no specific IP binding)
* Start Apache service inside the container
* Ensure container remains in running state

---

## 🎯 Objective

* Execute commands inside a running container
* Install and configure services within container
* Validate service functionality

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash id="f7x2pq"
ssh tony@stapp01
```

---

### 2️⃣ Switch to Root User

```bash id="k9d3mz"
sudo su -
```

---

### 3️⃣ Verify Running Container

```bash id="v4s8lw"
docker ps
```

Ensure container `kkloud` is running.

---

### 4️⃣ Access Container Shell

```bash id="n3p7yt"
docker exec -it kkloud bash
```

---

### 5️⃣ Update Package Index

```bash id="b2m6rc"
apt update
```

---

### 6️⃣ Install Apache

```bash id="z8k1qa"
apt install -y apache2
```

---

### 7️⃣ Configure Apache Port

Edit ports configuration file:

```bash id="d5w3cn"
vi /etc/apache2/ports.conf
```

Change:

```id="u9p2gh"
Listen 80
```

To:

```id="y7r4kl"
Listen 8088
```

---

### 8️⃣ Update Virtual Host Configuration

```bash id="w1c8po"
vi /etc/apache2/sites-available/000-default.conf
```

Change:

```id="p8m6fa"
<VirtualHost *:80>
```

To:

```id="r3v9zx"
<VirtualHost *:8088>
```

---

### 9️⃣ Start Apache Service

```bash id="h2q5lx"
service apache2 start
```

---

### 🔟 Verify Apache is Running

```bash id="x6d4nv"
service apache2 status
```

---

### 1️⃣1️⃣ Exit Container

```bash id="j4p8ws"
exit
```

---

### 1️⃣2️⃣ Verify Container is Still Running

```bash id="t2m7ka"
docker ps
```

---

## 🧪 Verification

Check if Apache is listening on port `8088` inside container:

```bash id="v9k3rd"
docker exec -it kkloud netstat -tulnp | grep 8088
```

---

## 🏁 Final Outcome

* Apache installed inside container
* Port changed to `8088`
* Service running successfully
* Container remains active

---

## 🔍 Key Concepts

| Concept         | Description                                  |
| --------------- | -------------------------------------------- |
| docker exec     | Run commands inside running container        |
| Container Shell | Interactive access to container              |
| Service Config  | Modify application settings inside container |
| Port Binding    | Define which port service listens on         |

---

## 💡 Key Learnings

* Executing commands inside containers
* Installing packages in running containers
* Modifying service configurations
* Managing services inside containers
* Verifying application inside container

---

## 🔁 Workflow

```bash id="o1k5rf"
docker exec → install → configure → start → verify
```

---

## 🚀 Summary

Used `docker exec` to configure Apache inside a running container — a practical approach for troubleshooting and quick updates in containerized environments.

---
