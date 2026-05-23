# ☸️ Day 50: Set Resource Limits in Kubernetes Pods

## 🧠 Problem Statement

The Nautilus DevOps team identified performance and resource management issues in Kubernetes-hosted applications. To avoid excessive resource consumption and ensure better workload stability, resource requests and limits need to be configured.

The task is to create a Kubernetes Pod running Apache (`httpd`) with defined CPU and memory resource constraints.

The `kubectl` utility is already configured on the **Jump Host Server**.

---

# 📋 Requirements

Create a Pod with the following specifications:

| Property       | Value             |
| -------------- | ----------------- |
| Pod Name       | `httpd-pod`       |
| Container Name | `httpd-container` |
| Image          | `httpd:latest`    |
| CPU Request    | `100m`            |
| Memory Request | `15Mi`            |
| CPU Limit      | `100m`            |
| Memory Limit   | `20Mi`            |

---

# 🎯 Objective

* Create a Kubernetes Pod
* Configure CPU and memory requests
* Configure CPU and memory limits
* Verify resource allocation in the cluster

---

# 🛠️ Implementation Steps

---

## 1️⃣ Connect to Jump Host

```bash id="a2m8qx"
ssh thor@jump-host
```

---

## 2️⃣ Create Pod YAML File

Create a new manifest file:

```bash id="v9p4kn"
vi httpd-pod.yaml
```

Add the following configuration:

```yaml id="r7x5bt"
apiVersion: v1
kind: Pod

metadata:
  name: httpd-pod

spec:
  containers:
  - name: httpd-container
    image: httpd:latest

    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"

      limits:
        memory: "20Mi"
        cpu: "100m"
```

---

## 3️⃣ Create Pod

Apply the manifest:

```bash id="f4w7cr"
kubectl apply -f httpd-pod.yaml
```

Expected output:

```bash id="q6t8mx"
pod/httpd-pod created
```

---

## 4️⃣ Verify Pod Status

```bash id="s9y3vb"
kubectl get pods
```

Expected output:

```bash id="d2m6pq"
NAME         READY   STATUS    RESTARTS   AGE
httpd-pod    1/1     Running   0          XXs
```

---

## 5️⃣ Verify Resource Allocation

Describe Pod:

```bash id="n5r8kx"
kubectl describe pod httpd-pod
```

Expected resource section:

```bash id="w4z7lj"
Limits:
  cpu:     100m
  memory:  20Mi

Requests:
  cpu:     100m
  memory:  15Mi
```

---

## 6️⃣ Additional Verification

Export Pod YAML:

```bash id="g8v2rs"
kubectl get pod httpd-pod -o yaml
```

---

# 🧪 Validation Commands

View all resources:

```bash id="c5p9tn"
kubectl get all
```

Check detailed Pod information:

```bash id="y2m4qx"
kubectl describe pod httpd-pod
```

---

# 🏁 Final Outcome

* Apache Pod created successfully
* CPU and memory requests configured
* CPU and memory limits configured
* Pod running successfully with controlled resource usage

---

# 🔍 Key Concepts

| Concept       | Description                             |
| ------------- | --------------------------------------- |
| Requests      | Minimum resources Kubernetes guarantees |
| Limits        | Maximum resources container can consume |
| CPU (`m`)     | Millicores (`100m = 0.1 CPU`)           |
| Memory (`Mi`) | Memory in Mebibytes                     |
| Pod           | Smallest deployable Kubernetes unit     |

---

# 💡 Key Learnings

* Configuring resource requests and limits
* Understanding CPU and memory allocation in Kubernetes
* Preventing resource overconsumption
* Improving application stability and performance
* Managing workloads efficiently in Kubernetes clusters

---

# 🔁 Workflow

```bash id="j7k4pw"
create YAML → apply manifest → verify pod → validate resource limits
```

---

# 🚀 Summary

Successfully deployed an Apache Pod with CPU and memory resource requests and limits. Resource management is an important Kubernetes concept because it helps maintain cluster stability and prevents workloads from consuming excessive resources.
