# Docker and Docker Compose

DevOps (Development and Operations) is a methodology that combines software development and IT operations to deliver applications faster, more reliably, and continuously. The focus is on automation—making processes such as testing, deployment, monitoring, and code integration run with minimal human intervention. Key DevOps principles include breaking down silos between developers and operations teams and using tools like Docker, Kubernetes, Jenkins, and Git to ensure automation and repeatability. A major emphasis is placed on CI/CD (Continuous Integration and Continuous Delivery), which allows teams to deploy updates quickly and safely.

One of the most important tools in this workflow is Docker Compose. Docker Compose simplifies the management of multi-container applications, allowing multiple services to run in isolated Docker containers but work together seamlessly. The YAML file used by Docker Compose defines:

The Docker images for each service

Port mappings to access services

Volumes for data persistence

Network configurations for inter-service communication

Dependencies to control the startup order of services

By using Docker Compose, developers can replicate a complex production-like environment on any machine with a single command: docker-compose up


## WHO IS WHO: 

In this project, we created a simulation of a real-world trading system. The system is composed of multiple services working together, designed to help us understand how modern data platforms are structured. It uses streaming and multiple databases to handle diverse types of data.

Services included in this setup:

Zookeeper – Coordinates Kafka brokers to manage distributed messaging.

Kafka – Handles real-time data streams and acts as a message broker between producers and consumers.

PostgreSQL – A relational database for structured transactional data.

Cassandra – A NoSQL database optimized for high-volume, distributed data.

InfluxDB – A time-series database designed for metrics and monitoring data.

Anaconda (Python environment) – A data science environment that can produce or consume Kafka streams, run analytics, and query the databases directly.

### How it works: Docker Compose reads the YAML file, launches all containers, creates a custom network for them to communicate, and sets up volumes so that data persists even if containers are removed. This guarantees consistency and makes the system portable.

<img width="1460" height="2220" alt="yaml file" src="https://github.com/user-attachments/assets/37d072ab-5e9f-4caf-9186-8e135688a65d" />

## Relationships and Connections

### Service interactions:

Zookeeper → Kafka: Kafka requires Zookeeper to manage its cluster and organize brokers.

Kafka → Databases: Kafka streams incoming data into PostgreSQL, Cassandra, and InfluxDB.

Anaconda ↔ Kafka & Databases: Anaconda can send (produce) data to Kafka, read (consume) data from Kafka, and query all databases directly for analytics or processing.

Network and Ports: All services communicate through the trading-net, a custom Docker network. Each service can be accessed externally via mapped ports:

| Service    | Default Port | Custom External Port |
| ---------- | ------------ | -------------------- |
| PostgreSQL | 5432         | 55432                |
| Cassandra  | 9042         | 19042                |
| InfluxDB   | 8086         | 18086                |
| Kafka      | 29092        | 29093                |
| Zookeeper  | 2181         | 2182                 |
| Anaconda   | 8888         | 18888                |

Data Persistence: Each service has a dedicated Docker volume to store data, ensuring that even if a container is deleted or restarted, no data is lost.

## Summary

This setup demonstrates a realistic, multi-service data system in a controlled environment using Docker Compose. It provides a reproducible environment where all services can interact seamlessly, making it easier to develop, test, and understand the behavior of distributed applications. By using custom ports, volumes, and a dedicated network, this setup is fully portable, safe, and ready for experimentation.


# 🐳Docker Desktop Installation & Setup

### Step 1 — Download Docker Desktop

1. #### Go to the Docker official website https://www.docker.com/products/docker-desktop
2. Download Docker Desktop for your OS (Windows, macOS, or Linux).
- For Windows: choose Download for Windows AMD64.
- For Mac: choose Intel Chip or Apple Silicon (M1/M2) version.
<img width="1600" height="916" alt="image" src="https://github.com/user-attachments/assets/31650c7d-47d4-40da-904b-268992e6ace4" />


### Step 2 — Install Docker Desktop

- Run the installer.
- Enable CPU virtualization from the bios system if its disabled
- Accept the license agreement and keep the default settings.
- Wait for installation to finish, then restart your computer if prompted.

<img width="1264" height="708" alt="image" src="https://github.com/user-attachments/assets/28a1beba-bfbc-4a13-98aa-450bcb11d3bf" />


### Step 3 — Creating a Project Folder
- Open a terminal and run: mkdir trading-tools-docker
- and run cd trading-tools-docker


<img width="1913" height="1028" alt="image" src="https://github.com/user-attachments/assets/000010d3-6aee-4579-911a-ba7cddedb0c7" />




