---

# 🐳 Day 42: Create a Docker Network

## 🧠 Problem Statement

The Nautilus DevOps team needs to create a custom Docker network on **Application Server 1 (`stapp01`)** to support containerized applications.

---

## 📋 Requirements

* Create a Docker network named `official`
* Use **bridge** network driver
* Configure subnet: `172.28.0.0/24`
* Configure IP range: `172.28.0.0/24`

---

## 🎯 Objective

* Create a custom Docker network
* Define IP addressing configuration
* Verify network setup

---

## 🛠️ Implementation Steps

---

### 1️⃣ Connect to Application Server

```bash id="k9w2zx"
ssh tony@stapp01
```

---

### 2️⃣ Switch to Root User

```bash id="r4m8qp"
sudo su -
```

---

### 3️⃣ Verify Docker Service

```bash id="t7x3kd"
systemctl status docker
```

Ensure it shows:

```id="q2v6nj"
active (running)
```

---

### 4️⃣ Create Docker Network

```bash id="m8p5ws"
docker network create \
--driver bridge \
--subnet 172.28.0.0/24 \
--ip-range 172.28.0.0/24 \
official
```

---

### 5️⃣ Verify Network Creation

```bash id="z3c7ry"
docker network ls
```

---

### 6️⃣ Inspect Network Details

```bash id="p6v1qo"
docker network inspect official
```

---

## 🧪 Verification

Check network configuration:

```bash id="n2k8sl"
docker network inspect official | grep -E "Subnet|IPRange"
```

---

## 🏁 Final Outcome

* Docker network `official` successfully created
* Bridge driver configured
* Subnet and IP range properly assigned
* Network verified

---

## 🔍 Key Concepts

| Concept        | Description                           |
| -------------- | ------------------------------------- |
| Bridge Network | Default Docker network for containers |
| Subnet         | Defines IP range for network          |
| IP Range       | Allocates IPs to containers           |
| docker network | Manages container networking          |

---

## 💡 Key Learnings

* Creating custom Docker networks
* Understanding container networking
* Managing IP allocation in Docker
* Using bridge networks for communication
* Verifying network configurations

---

## 🔁 Workflow

```bash id="f1t6mp"
create network → configure subnet → verify → inspect
```

---

## 🚀 Summary

Created a custom Docker bridge network with defined subnet and IP range — an essential step for managing communication between containers in real-world DevOps environments.

---
