## Microservices-Task 
# 🐬 Microservices Containerization with Node.js, Docker & Docker Compose
=======

---

## Overview

This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

The system consists of four independent services that communicate over an internal Docker network:

| Service | Description | Port |

|----------|--------------|------|

| **User Service** | Manages user data | 3000 |

| **Product Service** | Handles product information | 3001 |

| **Order Service** | Processes user orders | 3002 |

| **Gateway Service** | API gateway that routes external requests to internal services | 3003 |

All services are containerized individually and orchestrated through Docker Compose.

---

## 🧩 Tech Stack

- **Node.js** -- Backend runtime
- **Express.js** -- REST API framework
- **Axios** -- HTTP client for inter-service communication
- **Docker** -- Containerization platform
- **Docker Compose** -- Multi-container orchestration

---

## Services and Endpoints

### **User Service**

- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**

    ```
    curl http://localhost:3000/users
    ```

    Or open in your browser: [http://localhost:3000/users](http://localhost:3000/users)

---

### **Product Service**

- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**

    ```
    curl http://localhost:3001/products
    ```

    Or open in your browser: [http://localhost:3001/products](http://localhost:3001/products)

---

### **Order Service**

- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**

    ```
    curl http://localhost:3002/orders
    ```

    Or open in your browser: [http://localhost:3002/orders](http://localhost:3002/orders)

---

### **Gateway Service**

- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**
    ```
    curl http://localhost:3003/api/users
    ```
  - **Products:**
    ```
    curl http://localhost:3003/api/products
    ```
  - **Orders:**
    ```
    curl http://localhost:3003/api/orders
    ```

---

## Instructions

1. Start all services using the `docker-compose` file:
   ```
   docker-compose up
   ```
2. Once the services are running, use the above endpoints to verify the functionality.

Happy testing!


---

## 🏗️ Project Structure
-----------------------

<pre class="overflow-visible!" data-start="1910" data-end="2115"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre!"><span><span>
submission/

├── user-service/

│ ├── app.js

│ ├── package.json

│ └── Dockerfile

├── product-service/

│ ├── app.js

│ ├── package.json

│ └── Dockerfile

├── order-service/

│ ├── app.js

│ ├── package.json

│ └── Dockerfile

├── gateway-service/

│ ├── app.js

│ ├── package.json

│ └── Dockerfile

├── docker-compose.yml

└── README.md

  </span></span></code></div></div></pre>

* * * * *


## 🧭 Project Architecture

Below diagram illustrates the communication flow and orchestration between all microservices using Docker Compose.

<img width="1360" height="418" alt="Screenshot from 2025-11-08 15-51-04" src="https://github.com/user-attachments/assets/c06cb12c-aa98-4175-b8b1-5d96dec5c84b" />

---

## ⚙️ Prerequisites

Before starting, ensure the following are installed:

- **Docker Engine** ≥ 20.x  
- **Docker Compose** ≥ 1.27 (or integrated Docker Compose v2)  
- **Git** for cloning the repository

---

### **Verify installation:**

`docker --version`

`docker-compose --version`

---

🧱 Setup & Installation

### **Clone the repository**

`git clone https://github.com/`<your-username>`/Microservices-Task_Skill_test.git`

`cd Microservices-Task_Skill_test/submission`

<img width="1312" height="165" alt="Screenshot from 2025-11-08 14-30-05" src="https://github.com/user-attachments/assets/eaf8c6bd-2e9a-4ddb-81b6-9a11209b6417" />

---
<img width="1312" height="566" alt="Screenshot from 2025-11-08 14-36-48" src="https://github.com/user-attachments/assets/29bda94b-a284-42f3-8b49-c1d03afb34ad" />

---

### **Build and start all services**

`docker-compose up --build -d`

<img width="1312" height="655" alt="Screenshot from 2025-11-08 14-49-18" src="https://github.com/user-attachments/assets/03c83b43-ba3c-48c0-b447-ab1199e9dddd" />

---

### **Verify running containers**

`docker-compose ps`

<img width="1358" height="740" alt="Screenshot from 2025-11-08 15-19-47" src="https://github.com/user-attachments/assets/72523176-1c87-41ab-920f-387f75c1081e" />


---

### **Check logs**

`docker-compose logs -f`

<img width="1307" height="161" alt="Screenshot from 2025-11-08 15-26-49" src="https://github.com/user-attachments/assets/026e93b4-d4e3-4c5f-8527-4c7cf4c81005" />


🔍 ### **Testing the Services**

✅ Health Check Endpoints

Service  Endpoint  Response

<img width="1364" height="195" alt="Screenshot from 2025-11-08 15-16-54" src="https://github.com/user-attachments/assets/93e44c72-0b4b-441c-9f6e-1296b8670c46" />

---

🌐 API Testing via Gateway

Fetch Users

`curl http://localhost:3003/api/users`

<img width="1360" height="202" alt="Screenshot from 2025-11-08 16-01-57" src="https://github.com/user-attachments/assets/0b96df43-ca9e-45b1-a07f-91010094409f" />


Fetch Products

`curl http://localhost:3003/api/products`

<img width="1360" height="202" alt="Screenshot from 2025-11-08 15-59-55" src="https://github.com/user-attachments/assets/51baf432-7b39-414a-81a7-a960d1fa61e0" />


Create an Order

`curl -X POST http://localhost:3003/api/orders
  -H "Content-Type: application/json"
  -d '{"userId":1,"productId":2}'`

Get All Orders

`curl http://localhost:3003/api/orders`

If all endpoints respond successfully, the system is fully operational.

---

🧰 ### **Common Commands**

Action  Command

Build & Run containers  `docker-compose up --build -d`

Stop containers  `docker-compose down`

View logs  `docker-compose logs -f`

Rebuild specific service  `docker-compose build user-service`

Access a container shell  `docker exec -it user-service sh`

Remove all containers & images  `docker-compose down --rmi all --volumes`

---

🧠 ### **Troubleshooting**

Issue  Possible Cause  Fix

Port 3000 already in use  Grafana or another service using port  Stop Grafana (sudo systemctl stop grafana-server) or change Grafana's port

<img width="735" height="541" alt="image" src="https://github.com/user-attachments/assets/2d85f9e1-b080-4506-9484-fb7d369b4fde" />

---


🏁 Conclusion
-------------

This project successfully demonstrates the core principles of **containerization, microservice communication, and orchestration using Docker and Docker Compose**.\
Each service --- User, Product, Order, and Gateway --- was independently containerized, networked, and executed as part of a cohesive multi-service environment.

Through this implementation, I gained practical hands-on experience in:

-   Structuring and isolating microservices for scalability and maintainability

-   Building and optimizing Docker images efficiently

-   Managing multi-container environments with Docker Compose

-   Resolving networking and port conflicts within containerized systems

-   Testing inter-service API communication using internal Docker DNS

This project reflects a complete DevOps workflow --- from **development to deployment**, **testing**, and **documentation**.


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
