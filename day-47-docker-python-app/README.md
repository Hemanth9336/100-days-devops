# 🐳 Day 47: Dockerize a Python Application

## 🧠 Problem Statement

The Nautilus DevOps team needs to Dockerize and deploy a Python application on **Application Server 2 (`stapp02`)**.

A `requirements.txt` file containing application dependencies is already available under:

```bash id="p4x7km"
/python_app/src/
```

The task is to

* Create a Dockerfile
* Build a custom image
* Deploy the application container
* Expose the application through port mapping

---

# 📋 Requirements

## Dockerfile Requirements

* Create Dockerfile under

```bash id="w8n2qa"
/python_app/Dockerfile
```

* Use any Python base image
* Install dependencies from `requirements.txt`
* Expose port `3000`
* Run `server.py` using `CMD`

---

## Deployment Requirements

* Build image

```bash id="f5v9tr"
nautilus/python-app
```

* Create container

```bash id="m2k7zp"
pythonapp_nautilus
```

* Map

```bash id="c8x4lu"
Host Port: 8095 → Container Port: 3000
```

---

# 🎯 Objective

* Dockerize Python application
* Build reusable image
* Deploy application container
* Verify application accessibility

---

# 🛠️ Implementation Steps

---

## 1️⃣ Connect to Application Server

```bash id="k7r3mv"
ssh steve@stapp02
```

---

## 2️⃣ Switch to Root User

```bash id="x5n8pt"
sudo su -
```

---

## 3️⃣ Navigate to Application Directory

```bash id="q9m2df"
cd /python_app
```

---

## 4️⃣ Verify Existing Files

```bash id="z4t7wc"
ls -R
```

Expected structure:

```bash id="p2v6rq"
src/
requirements.txt
server.py
```

---

## 5️⃣ Create Dockerfile

```bash id="d7n1ys"
vi Dockerfile
```

---

## 6️⃣ Add Dockerfile Content

```dockerfile id="h3q8la"
FROM python:3.9

WORKDIR /app

COPY src/requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY src/ .

EXPOSE 3000

CMD ["python", "server.py"]
```

---

# 🔍 Dockerfile Breakdown

| Instruction | Purpose                   |
| ----------- | ------------------------- |
| FROM        | Uses Python base image    |
| WORKDIR     | Sets working directory    |
| COPY        | Copies application files  |
| RUN         | Installs dependencies     |
| EXPOSE      | Declares application port |
| CMD         | Starts Python application |

---

# 🏗️ Build Docker Image

```bash id="u8c4vw"
docker build -t nautilus/python-app .
```

---

# 🚀 Run Docker Container

```bash id="r5x9nm"
docker run -d \
--name pythonapp_nautilus \
-p 8095:3000 \
nautilus/python-app
```

---

# ✅ Verify Running Container

```bash id="b1m7qk"
docker ps
```

Expected output should include:

```bash id="e4v2lt"
pythonapp_nautilus
```

---

# 🧪 Test Application

```bash id="y7k3px"
curl http://localhost:8095/
```

Expected: Application response from `server.py`

---

# 🏁 Final Outcome

* Python application successfully Dockerized
* Custom image built successfully
* Container deployed and running
* Port mapping configured correctly
* Application accessible via browser/curl

---

# 🔍 Key Concepts

| Concept           | Description                       |
| ----------------- | --------------------------------- |
| Dockerfile        | Blueprint for container images    |
| Python Base Image | Runtime environment for app       |
| Port Mapping      | Exposes app outside container     |
| CMD               | Defines container startup command |
| pip install       | Installs Python dependencies      |

---

# 💡 Key Learnings

* Dockerizing Python applications
* Managing dependencies using `requirements.txt`
* Building reusable container images
* Deploying applications with Docker
* Exposing containerized services externally

---

# 🔁 Workflow

```bash id="v6p2ra"
write Dockerfile → build image → run container → verify app
```

---

# 🚀 Summary

Successfully Dockerized and deployed a Python application using Docker — including dependency management, custom image creation, and external access through port mapping.

This is a foundational real-world DevOps workflow for deploying modern applications in containers.
