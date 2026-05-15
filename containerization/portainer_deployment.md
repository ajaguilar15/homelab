# 🐳 Portainer Setup on Ubuntu Server

## Overview

This document outlines the deployment of Portainer inside Docker on an Ubuntu Server virtual machine running in VMware Workstation.

Portainer provides a web-based interface for managing:
- Docker containers
- Images
- Volumes
- Networks
- Infrastructure services

This marks the transition from:
```text
Basic Linux Administration
```

to:
```text
Containerized Infrastructure Management
```

---

## 📚 Concepts Learned

- Docker containers
- Docker volumes
- Docker daemon permissions
- Port mapping
- Persistent storage
- HTTPS services
- Self-signed SSL certificates
- Infrastructure management dashboards

---

## 🧱 Infrastructure Architecture

```text
Windows Host
└── VMware Workstation
    └── Ubuntu Server VM
        └── Docker Engine
            └── Portainer Container
```

---


## 🔧 Step 1 — Add User to Docker Group

```bash
sudo usermod -aG docker $USER
```

Apply new group membership:

```bash
newgrp docker
```

Expected output:

```text
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

---

## 🔧 Step 2 — Create Persistent Docker Volume

```bash
docker volume create portainer_data
```

Purpose:
- Stores Portainer configuration data persistently
- Prevents data loss if container is recreated

---

## 🔧 Step 3 — Deploy Portainer Container

```bash
docker run -d \
  --name portainer \
  --restart=unless-stopped \
  -p 8000:8000 \
  -p 9443:9443 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

---

## 🔧 Step 4 — Verify Running Container

```bash
docker ps
```

Expected output:

```text
CONTAINER ID   IMAGE                           STATUS
xxxxxxxxxxxx   portainer/portainer-ce:latest  Up
```

---

## 🔧 Step 5 — Determine Server IP Address

```bash
hostname -I
```

Important:
- `192.168.x.x` = server LAN IP
- `172.17.x.x` = Docker internal bridge network

Use the LAN IP.

Docker automatically created an internal bridge network:

```text
172.17.x.x
```

This demonstrates:
- container isolation
- internal Docker networking
- virtual network bridges

---

## 🔧 Step 6 — Access Portainer Web Interface

Open browser:

```text
https://192.168.75.129:9443
```

---

### ⚠️ SSL Warning Encountered

Browser displayed:

```text
Connection is not secure
```

Cause:
- Portainer automatically generates a self-signed SSL certificate

This is normal in homelab environments.

Encryption still functions correctly.

---

## 🔧 Step 7 — Initial Portainer Configuration

Actions completed:
1. Created administrator account
2. Connected to local Docker environment
3. Entered Portainer dashboard successfully

---

## 📂 Docker Resources Managed by Portainer

Portainer allows management of:
- Containers
- Images
- Volumes
- Networks
- Stacks
- Environments

---

## 🚀 Planned Future Containers

| Service | Purpose |
|---|---|
| PostgreSQL | Database |
| Nextcloud | Cloud storage |
| Homarr | Dashboard |
| Grafana | Monitoring |
| Prometheus | Metrics |
| NGINX Proxy Manager | Reverse proxy |