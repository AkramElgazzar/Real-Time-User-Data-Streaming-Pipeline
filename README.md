# Real-Time-User-Data-Streaming-Pipeline
This pipeline ingests real-time user data from the Random User API, processes it using Spark Streaming, orchestrates workflows with Airflow, and stores the processed data in Cassandra for scalable and fault-tolerant querying.  

## Architecture  
![System Architecture](architecture.png) 

```mermaid
graph LR
    A[RandomUser API] --> B[Airflow]
    B --> C[Kafka Producer]
    C --> D[(Kafka Cluster)]
    D --> E[Spark Streaming]
    E --> F[(Cassandra)]
```
The project integrates several essential technologies:  
- **Apache Airflow**: Orchestrates the data pipeline and schedules API data fetching.  
- **Apache Kafka & Zookeeper**: Handles real-time data streaming and message queuing.  
- **Apache Spark**: Processes streaming data with powerful distributed computing.  
- **PostgreSQL**: Stores Airflow metadata and serves as a relational database.  
- **Cassandra**: Provides a NoSQL database solution for storing processed data.  
- **Docker**: Containerizes all components for easy deployment and scalability.  

## Key Features  
- Real-time data ingestion from external API sources.  
- Fault-tolerant streaming with Kafka.  
- Distributed data processing with Spark.  
- Containerized deployment with Docker Compose.  
- End-to-end pipeline orchestration with Airflow.  
- Scalable data storage with Cassandra.  

## Challenges and Solutions  

### Challenge 1: Network Connectivity Between Containers  
**Problem**: Services like Airflow scheduler and webserver had difficulty connecting to the PostgreSQL database and other services due to DNS resolution issues within the Docker network.  

**Solution**: Implemented proper network configuration in the Docker Compose file, ensuring all services could communicate effectively.  

### Challenge 2: Dependency Management  
**Problem**: Conflicting Python dependencies between different services caused installation failures and runtime errors.  

**Solution**: Carefully managed `requirements.txt` files and container paths to ensure proper dependency installation across all services.  

### Challenge 3: Service Orchestration  
**Problem**: Services needed to start in the correct order with proper health checks to ensure system stability.  

**Solution**: Implemented dependency conditions and health checks in Docker Compose to ensure services start in the correct sequence and only when dependencies are fully operational.  

## Getting Started  

### Prerequisites  
- Docker and Docker Compose.  
- At least 4GB RAM available for Docker.

### Installation  
1. Clone the repository:  
   ```bash  
   git clone https://github.com/AkramElgazzar/Real-Time-User-Data-Streaming-Pipeline.git  
   cd Real-Time-User-Data-Streaming-Pipeline  
   ``` 

2. Start the services:  
   ```bash  
   docker-compose up -d  
   ```  

3. Access the interfaces:  
   - Airflow UI: `http://localhost:8080`  
   - Kafka Control Center: `http://localhost:9021`  
   - Spark Master UI: `http://localhost:9090`  

### Usage  
1. Log in to Airflow UI with default credentials (`airflow/airflow`).  
2. Enable the `user_automation` DAG.  
3. Monitor data flow through Kafka Control Center.  
4. Query processed data in Cassandra.  


## Future Enhancements  
- Add data visualization layer with Grafana or Superset.  
- Implement real-time analytics with Spark Streaming.  
- Add monitoring and alerting with Prometheus and Grafana.  
- Enhance security with proper authentication and encryption.  
 
