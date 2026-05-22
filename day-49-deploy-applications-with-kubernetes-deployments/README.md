# ☸️ Day 49: Deploy Applications with Kubernetes Deployments

## 🧠 Problem Statement

The Nautilus DevOps team is continuing its Kubernetes journey by deploying applications using **Kubernetes Deployments**.

The task is to create an Apache (`httpd`) deployment using the latest image and verify Kubernetes resources created automatically by the deployment.

The `kubectl` utility is already configured on the **Jump Host Server**.

---

# 📋 Requirements

Create a deployment with the following specifications:

| Property        | Value          |
| --------------- | -------------- |
| Deployment Name | `httpd`        |
| Image           | `httpd:latest` |
| Image Tag       | `latest`       |

---

# 🎯 Objective

* Create a Kubernetes Deployment
* Deploy Apache (`httpd`) application
* Verify Pods and ReplicaSets
* Scale application replicas

---

# 🛠️ Implementation Steps

---

## 1️⃣ Connect to Jump Host

```bash
ssh thor@jump-host
```

---

## 2️⃣ Create Deployment

Create deployment directly using `kubectl`:

```bash
kubectl create deploy httpd --image=httpd:latest
```

Expected output:

```bash
deployment.apps/httpd created
```

---

## 3️⃣ Verify Running Pods

```bash
kubectl get po
```

Expected output:

```bash
NAME                      READY   STATUS    RESTARTS   AGE
httpd-xxxxxxxxxx-xxxxx    1/1     Running   0          XXs
```

---

## 4️⃣ Verify Deployment

```bash
kubectl get deploy
```

Expected output:

```bash
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
httpd    1/1     1            1           XXs
```

---

## 5️⃣ Verify ReplicaSet

```bash
kubectl get rs
```

Expected output:

```bash
NAME                 DESIRED   CURRENT   READY   AGE
httpd-xxxxxxxxxx     1         1         1       XXs
```

---

## 6️⃣ Scale Deployment

Increase replicas to 3:

```bash
kubectl scale deploy httpd --replicas=3
```

Expected output:

```bash
deployment.apps/httpd scaled
```

---

## 7️⃣ Verify Updated Pods

```bash
kubectl get po
```

Expected output:

```bash
NAME                      READY   STATUS    RESTARTS   AGE
httpd-xxxxxxxxxx-abc12    1/1     Running   0          XXs
httpd-xxxxxxxxxx-def34    1/1     Running   0          XXs
httpd-xxxxxxxxxx-ghi56    1/1     Running   0          XXs
```

---

# 🧪 Validation Commands

Check deployment details:

```bash
kubectl describe deploy httpd
```

Check cluster resources:

```bash
kubectl get all
```

---

# 🏁 Final Outcome

* Apache deployment created successfully
* Pod created automatically by Deployment
* ReplicaSet generated automatically
* Deployment scaled from **1 → 3 replicas**
* Multiple Pods running successfully

---

# 🔍 Key Concepts

| Concept    | Description                             |
| ---------- | --------------------------------------- |
| Pod        | Smallest deployable Kubernetes unit     |
| Deployment | Manages application lifecycle           |
| ReplicaSet | Maintains desired Pod count             |
| Scaling    | Increasing/decreasing running instances |
| kubectl    | Kubernetes command line utility         |

---

# 💡 Key Learnings

* Creating deployments directly using CLI
* Understanding relationship between Deployment → ReplicaSet → Pod
* Scaling applications in Kubernetes
* Verifying resources with `kubectl` commands
* Learning Kubernetes self-healing and scaling concepts

---

# 🔁 Workflow

```bash
create deployment → verify pod → verify ReplicaSet → scale deployment → validate replicas
```

---

# 🚀 Summary

Successfully deployed an Apache application using Kubernetes Deployment and scaled it from one to three replicas. This demonstrates Kubernetes' ability to automatically manage application lifecycle, availability, and scalability in real-world environments.
