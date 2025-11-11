# Apache Superset Docker Setup

This folder contains the Docker configuration for running Apache Superset.

## Prerequisites

- Docker
- Docker Compose

## Quick Start

1. **Build and start the containers:**
   ```bash
   cd SSDOCKER
   docker-compose up -d
   ```

2. **Access Superset:**
   - URL: http://localhost:8088
   - Username: `admin`
   - Password: `admin`

## Configuration

### Default Credentials
- **Username:** admin
- **Password:** admin
- **Email:** admin@superset.com

**⚠️ IMPORTANT:** Change these credentials in production!

### Environment Variables

You can modify the following in `docker-compose.yml`:

- `SUPERSET_SECRET_KEY`: Secret key for Flask sessions (change in production)
- Database credentials (PostgreSQL)
- Redis configuration

### Custom Configuration

Edit `superset_config.py` to customize Superset behavior, including:
- Row limits
- Cache configuration
- Feature flags
- Celery settings for async queries

## Services

The setup includes three services:

1. **superset**: Main Superset application (port 8088)
2. **db**: PostgreSQL database for metadata
3. **redis**: Redis for caching and Celery message broker

## Volumes

- `db_data`: PostgreSQL data persistence
- `redis`: Redis data persistence
- `./superset_home`: Superset home directory

## Common Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f superset

# Restart Superset
docker-compose restart superset

# Rebuild after config changes
docker-compose up -d --build
```

## Troubleshooting

If you encounter issues:

1. Check logs: `docker-compose logs -f`
2. Restart services: `docker-compose restart`
3. Rebuild: `docker-compose up -d --build`
4. Reset everything: `docker-compose down -v` (⚠️ deletes all data)

## Production Considerations

Before deploying to production:

1. Change `SUPERSET_SECRET_KEY` to a strong random value
2. Update admin credentials
3. Configure proper database backups
4. Set up SSL/TLS termination
5. Review and harden security settings
6. Configure proper logging and monitoring
