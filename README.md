# MongoDB Docker Setup

This repository contains a Docker Compose configuration for running MongoDB in a container with network access, along with Mongo Express for web-based database management.

## Prerequisites

- Docker
- Docker Compose
- sudo access (for initial setup)

## Setup Instructions

1. Clone this repository or copy the `docker-compose.yml` file to your desired location.

2. Start the MongoDB container and Mongo Express:
```bash
sudo docker compose up -d
```

3. Allow external connections (required for network access):
```bash
sudo iptables -I DOCKER-USER -p tcp --dport 27017 -j ACCEPT
sudo iptables -I DOCKER-USER -p tcp --dport 8081 -j ACCEPT
```

## Connection Details

### MongoDB Connection

#### Local Connection
To connect from the host machine:
```
mongodb://admin:password123@localhost:27017
```

#### Network Connection
To connect from other machines on the network:
```
mongodb://admin:password123@<HOST_IP>:27017
```
Replace `<HOST_IP>` with the IP address of the machine running the container.

### Mongo Express Web Interface

#### Local Access
To access Mongo Express from the host machine:
```
http://localhost:8081
```

#### Network Access
To access Mongo Express from other machines on the network:
```
http://<HOST_IP>:8081
```
Replace `<HOST_IP>` with the IP address of the machine running the container.

## Default Credentials

- MongoDB Username: `admin`
- MongoDB Password: `password123`

## Security Notes

1. The default credentials should be changed in production
2. The ports 27017 (MongoDB) and 8081 (Mongo Express) are exposed to the network
3. Make sure your network is secure before exposing MongoDB and Mongo Express
4. Consider setting up authentication for Mongo Express in production

## Troubleshooting

If you encounter connection issues:

1. Verify the containers are running:
```bash
sudo docker ps
```

2. Check if the ports are accessible locally:
```bash
telnet localhost 27017  # For MongoDB
telnet localhost 8081   # For Mongo Express
```

3. Verify network connectivity:
```bash
ping <HOST_IP>
```

4. Check iptables rules:
```bash
sudo iptables -L
```

## Stopping the Containers

To stop the MongoDB and Mongo Express containers:
```bash
sudo docker compose down
```

## Data Persistence

Data is persisted using a Docker volume named `mongodb_data`. This ensures your data remains even if the containers are stopped or removed. 