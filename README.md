# Bookmark Deployment

A containerized deployment solution for the Bookmark application, featuring a modern microservices architecture with Redis caching, a high-performance API service, and an interactive portal frontend.

## Architecture Overview

```
┌─────────┐
│  User   │
└────┬────┘
     │ HTTP/API Requests
     ▼
┌──────────────────────┐
│      Nginx           │
│   (Reverse Proxy)    │
└──┬─────────┬─────────┘
   │         │
   ▼         ▼
┌──────────────┐  ┌────────────┐
│   Portal     │  │  Bookmark  │
│  (Frontend)  │  │  Service   │
└──────────────┘  └──────┬─────┘
                         │
                         ▼
                    ┌─────────┐
                    │  Redis  │
                    │ (Cache) │
                    └─────────┘
```

## Services

### Nginx (Reverse Proxy)
- **Port:** 80
- **Role:** Routes requests to appropriate services
- **Configuration:** [nginx/nginx.conf](nginx/nginx.conf)

### Bookmark Service (API Backend)
- **Port:** 8080
- **Image:** `toanpham123/bookmark_service:dev`
- **Dependencies:** Redis
- **Environment:** Configured via `.env` file

### Portal (Frontend)
- **Port:** 3000 (internal)
- **Image:** `ebvn/bookmark-app-portal:dev`
- **Role:** Interactive user interface for bookmark management

### Redis (Cache Layer)
- **Port:** 6379 (internal)
- **Image:** `redis:alpine`
- **Data Persistence:** Volume-mounted at `/data`

## Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) (v20.10+)
- [Docker Compose](https://docs.docker.com/compose/) (v1.29+)
- Port 80 available on host machine

### 2. Start Services
```bash
docker compose up -d
```

### 3. Access Application
- **Portal:** http://localhost
- **API:** http://localhost/api/

## License

[Add your license information here]