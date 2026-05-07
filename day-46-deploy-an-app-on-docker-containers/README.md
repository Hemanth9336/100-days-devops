# 🚀 Day 46 - Deploy an App on Docker Containers

## 📌 Task Overview

The Nautilus Application Development team wanted to deploy a PHP application using Docker containers with a complete multi-container setup using Docker Compose.

The task was to configure:

* A **PHP Apache web container**
* A **MariaDB database container**
* Proper **port mappings**
* Persistent **volume mappings**
* Environment variables for database configuration

The deployment needed to be tested on **App Server 2** before moving to production.

---

# 🏗️ Infrastructure Details

| Server               | Hostname  | Purpose                      |
| -------------------- | --------- | ---------------------------- |
| Application Server 2 | `stapp02` | Hosts Nautilus Application 2 |

---

# 🎯 Requirements

## Web Service

* Container Name: `php_blog`
* Image: `php:<apache-tag>`
* Port Mapping:

```bash
8088:80
```

* Volume Mapping:

```bash
/var/www/html:/var/www/html
```

---

## DB Service

* Container Name: `mysql_blog`
* Image: `mariadb`
* Port Mapping:

```bash
3306:3306
```

* Volume Mapping:

```bash
/var/lib/mysql:/var/lib/mysql
```

* Environment Variables:

  * `MYSQL_DATABASE=database_blog`
  * Custom DB user
  * Complex password

---

# 🛠️ Steps Performed

## 1️⃣ Login to App Server 2

```bash
ssh steve@stapp02
```

---

## 2️⃣ Create Docker Compose Directory

```bash
sudo mkdir -p /opt/dba
```

---

## 3️⃣ Create Docker Compose File

```bash
sudo vi /opt/dba/docker-compose.yml
```

---

# 📄 Docker Compose Configuration

```yaml
version: '3.8'

services:

  web:
    image: php:apache
    container_name: php_blog
    ports:
      - "8088:80"
    volumes:
      - /var/www/html:/var/www/html

  db:
    image: mariadb:latest
    container_name: mysql_blog
    ports:
      - "3306:3306"
    volumes:
      - /var/lib/mysql:/var/lib/mysql
    environment:
      MYSQL_DATABASE: database_blog
      MYSQL_USER: blog_user
      MYSQL_PASSWORD: Str0ngPass@123
      MYSQL_ROOT_PASSWORD: RootPass@123
```

---

# ▶️ Deploy the Stack

Run the following command from `/opt/dba`:

```bash
cd /opt/dba
sudo docker compose up -d
```

---

# 🔍 Verify Containers

```bash
sudo docker ps
```

Expected containers:

```bash
php_blog
mysql_blog
```

---

# 🌐 Test Application Access

```bash
curl http://localhost:8088/
```

Or:

```bash
curl http://<server-ip>:8088/
```

Expected output:

```html
<html>
...
Apache2 Debian Default Page
...
</html>
```

---

# ✅ Key Concepts Practiced

* Docker Compose multi-container deployment
* Container networking
* Port mapping
* Persistent storage with volumes
* Environment variable configuration
* PHP Apache container deployment
* MariaDB container setup

---

# 📚 Useful Commands

## Stop Containers

```bash
sudo docker compose down
```

---

## Restart Stack

```bash
sudo docker compose restart
```

---

## View Logs

```bash
sudo docker compose logs
```

---

## Check Running Containers

```bash
sudo docker ps
```

---

# 🎉 Outcome

Successfully deployed a multi-container application stack using Docker Compose with:

* PHP Apache Web Server
* MariaDB Database
* Persistent storage
* External port exposure
* Environment-based DB configuration

This setup simulates a real-world containerized application deployment environment used in DevOps workflows.
