# MongoDB Docker Setup

This repository contains a Docker Compose configuration for running MongoDB in a container with network access.

## Prerequisites

- Docker
- Docker Compose
- sudo access (for initial setup)

## Setup Instructions

1. Clone this repository or copy the `docker-compose.yml` file to your desired location.

2. Start the MongoDB container:
```bash
sudo docker compose up -d
```

3. Allow external connections (required for network access):
```bash
sudo iptables -I DOCKER-USER -p tcp --dport 27017 -j ACCEPT
```

## Connection Details

### Local Connection
To connect from the host machine:
```
mongodb://admin:password123@localhost:27017
```

### Network Connection
To connect from other machines on the network:
```
mongodb://admin:password123@<HOST_IP>:27017
```
Replace `<HOST_IP>` with the IP address of the machine running the container.

## Default Credentials

- Username: `admin`
- Password: `password123`

## Security Notes

1. The default credentials should be changed in production
2. The port 27017 is exposed to the network
3. Make sure your network is secure before exposing MongoDB

## Troubleshooting

If you encounter connection issues:

1. Verify the container is running:
```bash
sudo docker ps
```

2. Check if the port is accessible locally:
```bash
telnet localhost 27017
```

3. Verify network connectivity:
```bash
ping <HOST_IP>
```

4. Check iptables rules:
```bash
sudo iptables -L
```

## Stopping the Container

To stop the MongoDB container:
```bash
sudo docker compose down
```

## Data Persistence

Data is persisted using a Docker volume named `mongodb_data`. This ensures your data remains even if the container is stopped or removed. 