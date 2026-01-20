# Kubernetes Ingress – Complete Guide (Zero to Hero)

## 📌 What is Ingress?

Ingress is a Kubernetes **API object** that manages **external HTTP/HTTPS traffic** and routes it to internal services based on **hostnames and paths**.

> Ingress provides **Layer 7 (HTTP/HTTPS)** routing for Kubernetes applications.

⚠️ Important: Ingress **does not work alone**. It requires an **Ingress Controller** (like NGINX) to function.

---

## 🚨 Why Ingress is Needed?

Without Ingress:

* Each service needs its own **NodePort** or **LoadBalancer**
* Multiple LoadBalancers = **high cloud cost**
* No path-based routing

With Ingress:

* **Single LoadBalancer** for multiple services
* Path-based & host-based routing
* SSL/TLS termination
* Production-ready traffic management

---

## 🧠 Ingress Architecture (Flow)

![Uploading ingress.png…]()

```

---

## 🧩 Core Components

### 1️⃣ Ingress Resource

* YAML configuration
* Defines routing rules
* Example: /ui → frontend, /api → backend

### 2️⃣ Ingress Controller

* Actual traffic handler
* Watches Ingress resources
* Applies rules

Common controllers:

* NGINX (most popular)
* Traefik
* HAProxy
* Cloud-specific (AWS ALB, GCP GLB)

---

## 📄 Sample Ingress YAML

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
spec:
  rules:
  - host: myapp.com
    http:
      paths:
      - path: /ui
        pathType: Prefix
        backend:
          service:
            name: ui-service
            port:
              number: 80
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 8080
```

---

## 🔐 TLS / HTTPS Support

Ingress supports:

* SSL termination
* HTTPS routing
* cert-manager integration

TLS handled at Ingress → Pods run HTTP internally

---

## 🆚 Ingress vs Service

| Feature          | Service    | Ingress           |
| ---------------- | ---------- | ----------------- |
| OSI Layer        | L4 (TCP)   | L7 (HTTP)         |
| Routing          | Port-based | Path / Host-based |
| TLS              | ❌          | ✅                 |
| Cost Efficient   | ❌          | ✅                 |
| Production Ready | ❌          | ✅                 |

---

## 🌍 Real-World Use Case

Microservices setup:

* /login → auth-service
* /orders → order-service
* /payments → payment-service

Benefits:

* Single public endpoint
* Centralized security
* Easy scaling & maintenance

---

## 🎯 Interview One-Liners

* Ingress works at Layer 7
* Ingress requires an Ingress Controller
* Ingress reduces cloud load balancer cost
* NGINX is the most commonly used Ingress Controller

---

## ⚠️ Common Mistakes

* Assuming Ingress works without a controller
* Using NodePort in production
* Confusing Service with Ingress
* Forgetting TLS configuration

---

## ✅ Key Takeaway

Ingress is a **traffic management layer** for Kubernetes that enables **secure, scalable, and cost-effective external access** to services.

---

📘 Part of DevOps Zero to Hero – Kubernetes Learning Path
