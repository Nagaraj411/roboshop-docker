# 🤖 Roboshop Microservices - Docker Setup
📦 Overview
This repo contains a production-ready multi-container setup for the Roboshop e-commerce platform, orchestrated using Docker and a shared custom bridge network (roboshop). Each microservice is isolated, scalable, and networked for seamless communication.

## 🧱 Network Configuration
    networks:
    default:
        driver: bridge
        name: roboshop
        external: true


* ✅ Uses an external Docker bridge network called roboshop
* 💬 Enables container-to-container communication without extra port mappings

* 🔧 Microservices Included
    | 🧩 **Service** | 🔗 **Depends On**         | 📸 **Docker Image**      |
    | -------------- | -------------------------- | ------------------------- |
    | `mongodb`      | —                          | `nagaraj411/mongodb:v1`   |
    | `catalogue`    | `mongodb`                  | `nagaraj411/catalogue:v1` |
    | `redis`        | —                          | `redis:7.0` *(official)*  |
    | `user`         | `mongodb`, `redis`         | `nagaraj411/user:v1`      |
    | `cart`         | `catalogue`, `redis`       | `nagaraj411/cart:v1`      |
    | `mysql`        | —                          | `nagaraj411/mysql:v1`     |
    | `shipping`     | `mysql`, `cart`            | `nagaraj411/shipping:v1`  |
    | `rabbitmq`     | —                          | `rabbitmq:3` *(official)* |
    | `payment`      | `user`, `cart`, `rabbitmq` | `nagaraj411/payment:v1`   |
    | `frontend`     | *All backend services*     | `nagaraj411/frontend:v1`  |




* ⚙️ Key Features
    - ✅ Custom Bridge Network – Isolated yet interconnected microservices
    - 🚀 Fast Deployment – Simple docker-compose up spins up the entire stack
    - 🔐 Environment Variables – Secured RabbitMQ credentials in payment service
    - 📞 Internal DNS – Services communicate by name (e.g., mongodb, redis, cart)


### 🏁 Getting Started
    🔧 Create Docker network
    docker network create roboshop

### 🚀 Launch all services
    docker-compose up -d

### 📦 Check running containers
    docker ps

### 🧹 Stop and remove containers
    docker-compose down