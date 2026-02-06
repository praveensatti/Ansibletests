### Readme

## Ansible deployment
This repository contains an Ansible playbook (`main.yaml`) with roles to:
- install Java
- configure WildFly
- deploy one or more WAR files
- validate deployment health

## Dockerized deployment
A Docker-based version of the deployment is now included.

### Files
- `docker/wildfly/Dockerfile`: builds a WildFly image and deploys a WAR from `WAR_URL`.
- `docker-compose.yml`: runs the container with configurable ports and log settings.
- `.env.example`: sample runtime configuration values.

### Run with Docker Compose
```bash
cp .env.example .env
docker compose up -d --build
```

### Configure different WARs and ports
Edit `.env` and change:
- `WAR_URL` (artifact URL)
- `WAR_NAME` (target deployed file name)
- `APP_PORT` and `MGMT_PORT` (host ports)
- `APP_LOGS_ROOT_DIR`, `APP_LOG_MODE`, and `HOST_LOG_DIR` for logs

### Run multiple app variants
You can run multiple differently-configured deployments by using different env files and compose project names.

Example:
```bash
docker compose --env-file .env.jenkins -p jenkins up -d --build
docker compose --env-file .env.shopizer -p shopizer up -d --build
```
