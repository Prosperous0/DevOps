# Docker and Docker Compose

DevOps (Development and Operations) is a methodology that combines software development and IT operations to deliver applications faster, more reliably, and continuously. The focus is on automation—making processes such as testing, deployment, monitoring, and code integration run with minimal human intervention. Key DevOps principles include breaking down silos between developers and operations teams and using tools like Docker, Kubernetes, Jenkins, and Git to ensure automation and repeatability. A major emphasis is placed on CI/CD (Continuous Integration and Continuous Delivery), which allows teams to deploy updates quickly and safely.

One of the most important tools in this workflow is Docker Compose. Docker Compose simplifies the management of multi-container applications, allowing multiple services to run in isolated Docker containers but work together seamlessly. The YAML file used by Docker Compose defines:

- The Docker images for each service
- Port mappings to access services
- Volumes for data persistence
- Network configurations for inter-service communication
- Dependencies to control the startup order of services

### By using Docker Compose, developers can replicate a complex production-like environment on any machine with a single command: docker-compose up


## WHO IS WHO: 

In this project, we created a simulation of a real-world trading system. The system is composed of multiple services working together, designed to help us understand how modern data platforms are structured. It uses streaming and multiple databases to handle diverse types of data.

Services included in this setup:

- Zookeeper – Coordinates Kafka brokers to manage distributed messaging.
- Kafka – Handles real-time data streams and acts as a message broker between producers and consumers.
- PostgreSQL – A relational database for structured transactional data.
- Cassandra – A NoSQL database optimized for high-volume, distributed data.
- InfluxDB – A time-series database designed for metrics and monitoring data.
- Anaconda (Python environment) – A data science environment that can produce or consume Kafka streams, run analytics, and query the databases directly.

### How it works:
Docker Compose reads the YAML file, launches all containers, creates a custom network for them to communicate, and sets up volumes so that data persists even if containers are removed. This guarantees consistency and makes the system portable.

<img width="1460" height="2220" alt="yaml file" src="https://github.com/user-attachments/assets/37d072ab-5e9f-4caf-9186-8e135688a65d" />

## Relationships and Connections

### Service interactions:

- Zookeeper → Kafka: Kafka requires Zookeeper to manage its cluster and organize brokers.

- Kafka → Databases: Kafka streams incoming data into PostgreSQL, Cassandra, and InfluxDB.

- Anaconda ↔ Kafka & Databases: Anaconda can send (produce) data to Kafka, read (consume) data from Kafka, and query all databases directly for analytics or processing.

- Network and Ports: All services communicate through the trading-net, a custom Docker network. Each service can be accessed externally via mapped ports:

| Service    | Default Port | Custom External Port |
| ---------- | ------------ | -------------------- |
| PostgreSQL | 5432         | 5432                |
| Cassandra  | 9042         | 9042                |
| InfluxDB   | 8086         | 8086                |
| Kafka      | 9092        | 9093                |
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


### Step 4 - Creating the docker-Compose.yml file
- We paste the Yaml. configuration into a text file saved on trading-tools-docker
  
<img width="1909" height="1033" alt="Screenshot 2025-10-06 141506" src="https://github.com/user-attachments/assets/fdc0ca51-27f0-4494-94e9-8889e2bf6c07" />


### Step 5: We use the Command: docker compose pull
- This downloads all necessary Docker images defined in the docker-compose.yaml file (Kafka, Cassandra, PostgreSQL, InfluxDB, Anaconda, etc.).
- The images are shown under the Images tab in Docker Desktop.

<img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/f4d521ee-dc48-439d-8a28-72e4c5a9d80a" />

<img width="1769" height="885" alt="image" src="https://github.com/user-attachments/assets/bf6e8ffa-37a0-4e83-b5be-0a9331135907" />


### Step 6: We use the Command: docker compose up
- Starts all services in detached mode (background).
- You can see the containers running in the Containers tab.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/4dc141eb-3158-422c-96b1-f6e84aaa3291" />

<img width="1852" height="981" alt="image" src="https://github.com/user-attachments/assets/f931cc3d-42e3-4122-9ade-5890ed5f7434" />

<img width="1852" height="1016" alt="image" src="https://github.com/user-attachments/assets/77bd895d-41aa-4068-9fbf-6b5bce0fd5a6" />


### Step 7: To Verify Everything is Running as intended 
- We use the command: docker ps
- it Lists all currently running containers.
- Each container will show its ports, status, and uptime.
- You should see something like:

<img width="1779" height="1018" alt="image" src="https://github.com/user-attachments/assets/7c623b8f-f06d-4687-81cf-a8e14492f635" />

### Step 8: 
- We first connect to the container using this command: docker exec -it postgres psql -U admin -d postgres
- Creating a New Project Database using the command: CREATE DATABASE tradingdb;
- Verify the Database Exists using this command: \l
- Connect to the New Database using: \c tradingdb
- After we are done, we exist using \q  then run the command: docker exec -it postgres psql -U admin -d tradingdb
 
<img width="1862" height="1019" alt="image" src="https://github.com/user-attachments/assets/bd8c6e25-0faf-41bc-bb7d-f4393b9ef940" />

### Step 9: Cassandra, Accessing each service
- We opened an interactive Cassandra CLI (cqlsh) inside the cassandra container.
- This is how we run CQL commands, inspect keyspaces/tables, or create schema
- By using this command: docker exec -it cassandra cqlsh

<img width="1853" height="1015" alt="image" src="https://github.com/user-attachments/assets/799e89f1-81f9-4101-88b8-fd788a56e3ec" />

### Step 10: Accesing InfluxDB
- we open ourbrowser, and access the website (localhost) : http://localhost:8086
- the credentials are in the Yaml. code file as shown below
<img width="441" height="275" alt="image" src="https://github.com/user-attachments/assets/a0eb1cd0-58cd-438f-aa8d-bbf4d7de81c2" />

- this is the homepage after logging in with our designated credentials
<img width="1913" height="1029" alt="image" src="https://github.com/user-attachments/assets/d408d788-07f8-4e86-a60a-1c85b8969474" />

### Step 11: Checking Conda 

- We opened a shell in the Anaconda container and checked conda --version. The screenshot shows either success or an error that conda is recognized

<img width="1437" height="595" alt="image" src="https://github.com/user-attachments/assets/2b181b89-784d-45d3-9f59-2baafc729f75" />

### Step 12: Netowrk

- All containers are connected through a custom Docker network (e.g., trading-net).
- 
- This allows inter-container communication using service names (like postgres, kafka, etc.) instead of IP addresses.

### Step 13: Volumes 

- Docker volumes are used to persist data so that it isn’t lost when containers are stopped or removed.
- To list all volumes: docker volume ls
- Common practice: each service has a mapped volume for storing its data (e.g., /var/lib/postgresql/data for PostgreSQL).
  
 <img width="1864" height="1019" alt="image" src="https://github.com/user-attachments/assets/1a579b46-0930-4af9-9259-fec661518920" />









