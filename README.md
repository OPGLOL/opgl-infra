# OPGL Docker Infrastructure Wrapper

Docker Compose configuration for running OPGL microservices locally.

## Services

| Service | Port | Description |
|---------|------|-------------|
| opgl-data-service | 8081 | Direct interface to Riot API |
| opgl-gateway-service | 8080 | API Gateway and orchestrator |
| opgl-cortex-engine-service | 8082 | AI/ML analysis engine |

## Prerequisites

- Docker and Docker Compose installed
- Riot Games API key ([Get one here](https://developer.riotgames.com/))

## Setup

1. Copy the environment template:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your Riot API key:
   ```
   RIOT_API_KEY=your-actual-api-key
   ```

## Usage

### Start all services
```bash
docker-compose up -d
```

### View logs
```bash
docker-compose logs -f
```

### View specific service logs
```bash
docker-compose logs -f opgl-gateway-service
```

### Stop all services
```bash
docker-compose down
```

### Rebuild and restart
```bash
docker-compose up -d --build
```

## Health Checks

All services expose health endpoints via POST:

```bash
curl -X POST http://localhost:8080/health  # Gateway
curl -X POST http://localhost:8081/health  # Data Service
curl -X POST http://localhost:8082/health  # Cortex Engine
```

## Network

All services communicate via the `opgl-network` Docker bridge network.
