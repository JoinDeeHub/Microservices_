 Microservices Kubernetes Deployment -- Skill Test 2
==================================================

**Container Orchestration (MCAD)**

* * * * *

Objective
---------

Deploy a Node.js microservices application on Kubernetes, ensuring proper configuration, service discovery, and inter-service communication.

This deployment was performed on an **on-prem Kubernetes cluster using Docker Desktop**, not on EKS or any cloud provider.

* * * * *

Application Architecture
------------------------

The application consists of four containerized Node.js microservices:

| Service Name | Port |
| --- | --- |
| User Service | 3000 |
| Product Service | 3001 |
| Order Service | 3002 |
| Gateway Service | 3003 |

<img width="1429" height="807" alt="diagram-export-14-12-2025-23_17_33" src="https://github.com/user-attachments/assets/7515a9f6-28d3-4bb5-b8de-724c0514da6c" />


* * * * *

Platform & Tools
----------------

-   Kubernetes (Docker Desktop -- On-Prem)

-   kubectl

-   Docker

-   NGINX Ingress Controller

* * * * *

Folder Structure
----------------

`submission/
├── deployments/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── ingress/
│   └── ingress.yaml
├── screenshots/
│   ├── pods.png
│   ├── service-test.png
│   └── logs.png
├── user-service/
├── product-service/
├── order-service/
└── gateway-service/`

* * * * *

Kubernetes Deployment Details
-----------------------------

### Deployments

Each Deployment includes:

-   Correct container image reference

-   Resource requests and limits

-   Environment variables

-   Liveness and readiness probes

-   Proper labels and selectors

### Services

-   All services use **ClusterIP**

-   Enables internal Kubernetes DNS-based service discovery

-   Correct port mapping for each microservice

* * * * *

Deployment Steps
----------------

`kubectl apply -f submission/deployments/
kubectl apply -f submission/services/
kubectl apply -f submission/ingress/ingress.yaml`

* * * * *

Verification & Testing
----------------------

### 1\. Verify Pods, Services, and Ingress

`kubectl get pods -o wide
kubectl get svc
kubectl get ingress`

* * * * *

### 2\. Inter-Service Communication Test (ClusterIP)

A temporary curl pod was used to validate Kubernetes DNS and service connectivity:

`kubectl run curlpod --image=curlimages/curl -it --restart=Never -- sh`

Inside the pod:

`nslookup user-service
curl -v http://user-service:3000`

This confirms:

-   Kubernetes DNS resolution

-   ClusterIP service discovery

-   TCP connectivity between services

> **Note:** HTTP `404 Not Found` responses are expected because the services do not expose a root (`/`) endpoint.\
> A `404` confirms that the service is reachable and the application is running.

* * * * *

### 3\. Gateway Logs (Service Communication)

`kubectl logs -l app=gateway-service --tail=100`

Gateway logs confirm communication with downstream services.

* * * * *

Ingress Configuration (Bonus Task)
----------------------------------

NGINX Ingress Controller was enabled and configured with the following routes:

| Path | Backend Service |
| --- | --- |
| `/api/users` | User Service |
| `/api/products` | Product Service |
| `/api/orders` | Order Service |
| `/` | Gateway Service |

Ingress Host:

`micro.local`

Ingress was tested using port-forwarding:

`kubectl -n ingress-nginx port-forward svc/ingress-nginx-controller 8080:80`

* * * * *

Screenshots
-----------

The following screenshots are included as evidence:

-   **pods.png** -- Running pods (`kubectl get pods -o wide`)

-   **service-test.png** -- DNS resolution and service connectivity test

-   **logs.png** -- Gateway service logs showing communication

* * * * *

Troubleshooting
---------------

### ImagePullBackOff

-   Ensure Docker images are built locally when using Docker Desktop Kubernetes:

`docker build -t user-service:latest ./submission/user-service`

### Curl Timeouts

-   Some services do not expose `/` or `/health` endpoints.

-   DNS resolution and TCP connectivity were used instead to validate service communication.

* * * * *

Conclusion
----------

All microservices were successfully deployed on Kubernetes with:

-   Proper service discovery

-   Internal communication using ClusterIP

-   Resource management and health probes

-   Optional ingress routing

This fulfills all requirements of **Skill Test 2 -- Container Orchestration**.


📸 Screenshots (Attach in Submission)

* * * * *

🧑‍💻 Author
------------

**DEEPIKA NARENDRAN**\
*DevOps Technical Lead | MCAD Program*\

[DevOps B13]
Skill Test 1 -- Cloud & Containers
Microservices Containerization Assignment

📧 deepika2.ytb@gmail.com\
💼 [GitHub: JoinDeeHub](https://github.com/JoinDeeHub)\
📍 Bengaluru, India
