# 🐘 PostgreSQL Database Setup

## Overview

This document outlines the setup of a PostgreSQL database container on an Ubuntu Server homelab using Docker.

---

## 🧱 Architecture

```text
Windows Host
└── VMware Workstation
    └── Ubuntu Server VM
        └── Docker Engine
            ├── Portainer
            └── PostgreSQL Container
                └── Database
```

---

## 📚 Concepts Learned

- Containerized databases
- PostgreSQL setup
- Docker volumes
- Environment variables
- Database authentication
- Persistent backend storage

---

## 🔧 Step 1 — Create PostgreSQL Volume

```bash
docker volume create postgres_data
```

Purpose:

```text
Stores PostgreSQL data outside of the container lifecycle.
```

---

## 🔧 Step 2 — Run PostgreSQL Container

```bash
docker run -d \
  --name postgres \
  --restart=unless-stopped \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=StrongPassword123 \
  -e POSTGRES_DB=SoftCover \
  -p 5432:5432 \
  -v postgres_data:/var/lib/postgresql \
  postgres:latest
```

---

## ⚠️ Issue Encountered

The first PostgreSQL container restarted repeatedly.

Docker showed:

```text
Restarting (1)
```

Logs showed an error related to PostgreSQL 18+ image behavior and the mounted path:

```text
/var/lib/postgresql/data
```

The issue occurred because newer PostgreSQL images expect the volume to be mounted at:

```text
/var/lib/postgresql
```

---

## 🔧 Fix Applied

The failed container and volume were removed:

```bash
docker stop postgres
docker rm postgres
docker volume rm postgres_data
```

Then the volume was recreated:

```bash
docker volume create postgres_data
```

The container was recreated using the corrected mount path:

```bash
-v postgres_data:/var/lib/postgresql
```

---

## 🔍 Verify Container Is Running

```bash
docker ps
```

Expected result:

```text
postgres   Up
```

---

## 🔍 Check Logs

```bash
docker logs postgres
```

Successful logs indicate that PostgreSQL initialized and is ready to accept connections.

---

## 🔧 Connect to PostgreSQL

```bash
docker exec -it postgres psql -U admin -d SoftCover
```

---

## 🧠 Key Takeaway

The database is now running as a containerized backend service.

```text
Application Data
↓
PostgreSQL Database
↓
Docker Volume
↓
Ubuntu Server Storage
↓
VMware Virtual Disk
```

---

## 🎯 Skills Developed

- PostgreSQL administration
- Dockerized database deployment
- Persistent volume management
- Troubleshooting container logs
- Understanding database storage paths

---

## 🚀 Next Steps

- Convert PostgreSQL setup to Docker Compose
- Add pgAdmin for database GUI management
- Connect a backend API to PostgreSQL
- Add automated database backups