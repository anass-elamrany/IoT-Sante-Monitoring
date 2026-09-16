# IoT Healthcare Monitoring System

This project is a simple IoT healthcare monitoring platform. It simulates patient vital signs, sends them through MQTT, stores the data in InfluxDB, and prepares the system for visualization with Grafana.

The project was developed as part of an Applied Computer Science S5 course.

## Overview

The system simulates remote monitoring for multiple patients. A Python script generates medical data such as heart rate, body temperature, oxygen saturation, and blood pressure. The data is published to an MQTT broker and can be processed, stored, and visualized using the included Docker services.

## Architecture

The project uses a basic IoT architecture:

1. Python simulator generates patient data.
2. Mosquitto receives data through MQTT.
3. Node-RED can process and route the data.
4. InfluxDB stores time-series medical data.
5. Grafana can display monitoring dashboards.

![Architecture Diagram](images/architecture.png)

## Technologies

| Component | Technology |
| --- | --- |
| Containers | Docker Compose |
| Simulator | Python 3 |
| Messaging | Eclipse Mosquitto |
| Processing | Node-RED |
| Database | InfluxDB 1.8 |
| Visualization | Grafana |

## Project Structure

```text
.
|-- docker-compose.yml
|-- images/
|   `-- architecture.png
|-- mosquitto/
|   `-- config/
|       `-- mosquitto.conf
`-- simulator/
    |-- patient_simulator.py
    `-- requirements.txt
```

## Requirements

- Docker and Docker Compose
- Python 3
- Git

## How to Run

Clone the repository:

```bash
git clone https://github.com/anass-elamrany/IoT-Sante-Monitoring.git
cd IoT-Sante-Monitoring
```

Start the services:

```bash
docker compose up -d
```

Install the simulator dependency:

```bash
cd simulator
pip install -r requirements.txt
```

Run the patient simulator:

```bash
python patient_simulator.py
```

## Service URLs

| Service | URL |
| --- | --- |
| Grafana | http://localhost:3000 |
| Node-RED | http://localhost:1880 |
| InfluxDB | http://localhost:8086 |
| Mosquitto MQTT | localhost:1883 |
| Mosquitto WebSocket | localhost:9001 |

Default Grafana login:

```text
Username: admin
Password: admin
```

## MQTT Data

The simulator publishes data to topics like:

```text
hopital/service_A/patient_001
hopital/service_A/patient_002
hopital/service_A/patient_003
```

Example message:

```json
{
  "id": "001",
  "bpm": 78,
  "temp": 37.1,
  "spo2": 98,
  "tension": "120/80",
  "timestamp": 1760000000
}
```

## Stop the Project

```bash
docker compose down
```
