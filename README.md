# MySQL Docker Setup for CRM Project

This repository provides a Docker setup to run a **MySQL 8.0** database for the CRM system.  
It is designed to work with:
- [crm-ui](https://github.com/DhandyF/crm-ui) (Frontend - Vue 2)
- [crm-api](https://github.com/DhandyF/crm-api) (Backend - Laravel 12)

---

## 📦 Features

- MySQL 8.0 in a container
- Custom credentials
- Data persistence using Docker volumes
- Exposes port **3308**
- Connects to shared external Docker network (`crm-network`)

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/mysql-docker.git
cd mysql-docker
```

### 2. Ensure External Network Exists
This setup assumes you are using a shared Docker network named crm-network.
If not already created, create it manually:
```bash
docker network create crm-network
```

### 2. Start MySQL Container

```bash
docker-compose up -d
```

This will start a MySQL server accessible at:
```yaml
Host: 127.0.0.1
Port: 3308
Database Name: crm
Username: user
Password: 123456
Root Password: root
```

> 🐳 If you're accessing the database from another Docker container (e.g., Laravel app), it will be available at:
> - Host: crm-db
> - Port: 3306 (container's internal port)

### 3. Stop MySQL Container

```bash
docker-compose down
```

---

## 🧩 Running the Full CRM Stack in Docker
To run the entire CRM application including the frontend, backend, and database, follow this order:

### 1. Start the Database First
```bash
docker-compose up -d  # Run from this repo
```

### 2. Start the Laravel API (crm-api)
Go to your crm-api directory and run:
```bash
docker-compose up -d --build
```

### 3. Start the Vue Frontend (crm-ui)
Go to your crm-ui directory and run:
```bash
docker-compose up -d --build
```
___

## 📋 System Approach

### Overview
CRM system is builded into three independent services—crm-ui, crm-api, and crm-db —using Docker Compose to manage and isolate each service. This approach aligns with modern software engineering best practices, offering flexibility, scalability, and clean separation of concerns.

By adopting a microservices-inspired approach with Docker Compose, each service can be developed, tested, and deployed independently. This modular design not only accelerates development but also lays a solid foundation for building scalable, maintainable, and cloud-ready applications.

### 🔧 Service Breakdown
1. **crm-ui (Frontend)**
- Framework: Vue.js (v2)
- Role: Responsible for the user interface and client-side interaction.
- Deployment: Built and served via Docker using an Nginx container.
- Interaction: Makes API calls to crm-api using Axios.

2. **crm-api (Backend)**
- Framework: Laravel (v12)
- Role: Acts as the core API layer for business logic and data processing.
- Database Access: Connects to the crm-db MySQL instance.
- Endpoints: Exposes RESTful API routes (e.g., /api/contact) for consumption by the frontend.

3. **crm-db (Database)**
- Database Engine: MySQL 8.0
- Role: Persistent data storage for the application.
- Isolation: Runs as a separate container to maintain data portability and separation.

### ✅ The advantages of this approach
➕ **Modularity & Separation of Concerns**

- Each service runs in its own container, allowing independent development, testing, and scaling. For example:
    - You can update or rebuild the frontend (crm-ui) without affecting the API or database.
    - The backend (crm-api) can evolve or change technologies independently.

➕ **Network Isolation with Shared Communication**

- By connecting services to a shared Docker external network, inter-service communication is seamless (e.g., Laravel connects to the DB using DB_HOST=crm-db).

➕ **Scalability**
- This structure sets the foundation for future scalability. For example:
    - Deploying frontend via CDN or serverless.
    - Containerizing backend with auto-scaling in Kubernetes or Docker Swarm.
    - Replacing MySQL with another database without affecting other layers.
