# ☸️ Day 48: Deploy Pods in Kubernetes Cluster

## 🧠 Problem Statement

The Nautilus DevOps team has started working with Kubernetes for container orchestration and application management.

The task is to create a Kubernetes Pod with specific image, labels, and container naming requirements using the Kubernetes cluster configured on the **Jump Host Server**.

---

# 📋 Requirements

Create a Pod with the following specifications

| Property       | Value             |
| -------------- | ----------------- |
| Pod Name       | `pod-httpd`       |
| Image          | `httpd:latest`    |
| Container Name | `httpd-container` |
| App Label      | `httpd_app`       |

---

# 🎯 Objective

* Create a Kubernetes Pod
* Assign labels to the Pod
* Configure a custom container name
* Deploy the Pod successfully in the cluster

---

# 🛠️ Implementation Steps

---

## 1️⃣ Connect to Jump Host

```bash
ssh thor@jump-host
```

---

## 2️⃣ Create Pod YAML File

Create a manifest file

```bash
vi pod-httpd.yaml
```

Add the following configuration

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: pod-httpd
  labels:
    app: httpd_app

spec:
  containers:
  - name: httpd-container
    image: httpd:latest
```

---

## 3️⃣ Deploy Pod

Apply the configuration

```bash
kubectl apply -f pod-httpd.yaml
```

Expected output

```bash
pod/pod-httpd created
```

---

## 4️⃣ Verify Pod Status

Check Pod details

```bash
kubectl get pods
```

Expected output

```bash
NAME         READY   STATUS    RESTARTS   AGE
pod-httpd    1/1     Running   0          XXs
```

---

## 5️⃣ Verify Labels

```bash
kubectl get pods --show-labels
```

Expected output

```bash
NAME         READY   STATUS    RESTARTS   AGE   LABELS
pod-httpd    1/1     Running   0          XXs   app=httpd_app
```

---

## 6️⃣ Verify Container Details

```bash
kubectl describe pod pod-httpd
```

Verify

```bash
Container Name: httpd-container
Image: httpd:latest
```

---

# 🧪 Validation Commands

Check all resources

```bash
kubectl get pods -o wide
```

Check Pod YAML

```bash
kubectl get pod pod-httpd -o yaml
```

---

# 🏁 Final Outcome

* Kubernetes Pod created successfully
* Apache (`httpd:latest`) container deployed
* Custom container name configured
* Labels added successfully
* Pod running inside Kubernetes cluster

---

# 🔍 Key Concepts

| Concept       | Description                                |
| ------------- | ------------------------------------------ |
| Pod           | Smallest deployable unit in Kubernetes     |
| Labels        | Key-value pairs used to organize resources |
| Container     | Application running inside Pod             |
| kubectl       | Command-line tool to manage Kubernetes     |
| YAML Manifest | Declarative resource configuration         |

---

# 💡 Key Learnings

* Creating Pods using YAML manifests
* Working with labels in Kubernetes
* Defining custom container names
* Managing workloads through `kubectl`
* Understanding Kubernetes resource structure

---

# 🔁 Workflow

```bash
create YAML → apply manifest → verify pod → validate labels
```

---

# 🚀 Summary

Successfully deployed an Apache Pod in Kubernetes with custom labels and container configuration — a foundational step toward learning Kubernetes resource management and container orchestration.
