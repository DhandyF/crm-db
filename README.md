# MySQL Docker Setup for CRM Project

This repository provides a Docker setup to run a **MySQL 8.0** database for the CRM system.  
It is designed to be used for local development, especially for applications like [CRM-API](https://github.com/DhandyF/crm-api) and other services via a shared Docker network..

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
