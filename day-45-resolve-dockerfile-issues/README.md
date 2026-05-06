# 🐳 Day 45: Resolve Dockerfile Issues

## 🧠 Problem Statement

The Nautilus DevOps team is working on building a custom Docker image on **Application Server 1 (`stapp01`)**.

A Dockerfile already exists under:

```bash id="v4n8qp"
/opt/docker/Dockerfile
```

However, the Docker image build is failing due to incorrect Apache configuration paths inside the Dockerfile.

The task is to troubleshoot and fix the Dockerfile without modifying:

* Base image
* Existing valid configurations
* Application data files (`index.html`, certificates, etc.)

---

## 📋 Existing Dockerfile (Problematic)

```dockerfile id="k2m7dx"
FROM httpd:2.4.43

RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf.d/httpd.conf

RUN sed -i '/LoadModule\ ssl_module modules\/mod_ssl.so/s/^#//g' conf.d/httpd.conf

RUN sed -i '/LoadModule\ socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' conf.d/httpd.conf

RUN sed -i '/Include\ conf\/extra\/httpd-ssl.conf/s/^#//g' conf.d/httpd.conf

COPY certs/server.crt /usr/local/apache2/conf/server.crt

COPY certs/server.key /usr/local/apache2/conf/server.key

COPY html/index.html /usr/local/apache2/htdocs/
```

---

# ❌ Root Cause

The Docker build failed because the Dockerfile was referencing an incorrect Apache configuration path:

```bash id="m9q4zs"
/usr/local/apache2/conf.d/httpd.conf
```

and

```bash id="r5w1tx"
conf.d/httpd.conf
```

The official Apache Docker image (`httpd:2.4.43`) does **not** contain a `conf.d` directory.

Correct Apache configuration file path:

```bash id="y3p8lv"
/usr/local/apache2/conf/httpd.conf
```

---

# ✅ Fixed Dockerfile

```dockerfile id="t7x2mn"
FROM httpd:2.4.43

RUN sed -i 's/Listen 80/Listen 8080/g' /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule ssl_module modules\/mod_ssl.so/s/^#//g' /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' /usr/local/apache2/conf/httpd.conf

RUN sed -i '/Include conf\/extra\/httpd-ssl.conf/s/^#//g' /usr/local/apache2/conf/httpd.conf

COPY certs/server.crt /usr/local/apache2/conf/server.crt

COPY certs/server.key /usr/local/apache2/conf/server.key

COPY html/index.html /usr/local/apache2/htdocs/
```

---

# 🛠️ Implementation Steps

---

## 1️⃣ Connect to Application Server

```bash id="n8v2cf"
ssh tony@stapp01
```

---

## 2️⃣ Switch to Root User

```bash id="q4r7mx"
sudo su -
```

---

## 3️⃣ Navigate to Docker Directory

```bash id="h2z9kp"
cd /opt/docker
```

---

## 4️⃣ Edit Dockerfile

```bash id="w5c1lt"
vi Dockerfile
```

Replace all incorrect paths:

```bash id="f7k3rd"
conf.d/httpd.conf
```

with:

```bash id="x1m8qs"
/usr/local/apache2/conf/httpd.conf
```

---

## 5️⃣ Build Docker Image

```bash id="p9v4ty"
docker build -t custom-httpd .
```

---

## 6️⃣ Verify Image Creation

```bash id="s3n7qx"
docker images
```

Expected output:

```bash id="b8t4md"
custom-httpd
```

---

# 🧪 Optional Verification

Run container:

```bash id="u8k2md"
docker run -d -p 8080:8080 custom-httpd
```

Test application:

```bash id="g4w9rl"
curl http://localhost:8080
```

---

# 🏁 Final Outcome

* Dockerfile issues fixed successfully
* Correct Apache configuration path used
* Docker image builds without errors
* Apache configured to listen on port `8080`
* Application accessible through container

---

# 🔍 Key Concepts

| Concept            | Description                             |
| ------------------ | --------------------------------------- |
| Dockerfile         | Instructions to build Docker images     |
| Apache Config Path | Main Apache configuration file location |
| sed                | Used to automate config changes         |
| COPY               | Copies files into Docker image          |
| docker build       | Builds image from Dockerfile            |

---

# 💡 Key Learnings

* Troubleshooting Docker build failures
* Understanding Apache structure inside containers
* Importance of correct file paths in Docker images
* Debugging Dockerfile step-by-step
* Using `sed` for automated configuration updates

---

# 🔁 Workflow

```bash id="z6m3pa"
inspect Dockerfile → identify invalid path → fix config → build image → verify
```

---

# 🚀 Summary

Resolved Dockerfile build failures caused by incorrect Apache configuration paths and successfully built a working custom Docker image — a practical troubleshooting task commonly faced in real-world DevOps environments.
