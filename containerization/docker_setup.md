# 🐳 Docker Installation and Setup on Ubuntu Server

Docker transforms the Ubuntu VM from a standalone Linux system into a containerized application platform capable of running:
- web applications
- databases
- dashboards
- monitoring tools
- APIs
- automation services

## 🧠 Docker Architecture

Ubuntu Server
      ↓
Docker Engine
      ↓
Containers
      ↓
Applications

## 🔧 Step 1 — Update Ubuntu

```bash
sudo apt update
sudo apt upgrade
```

## 🔧 Step 2 — Install Required Dependencies
```bash
sudo apt install ca-certificates curl gnupg lsb-release
```

## 🔧 Step 3 — Add Docker GPG Key
```bash
sudo mkdir -p /etc/apt/keyrings
```
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

## 🔧 Step 4 — Add Docker Repository
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 🔧 Step 5 — Refresh Package Lists
```bash
sudo apt update
```

## 🔧 Step 6 — Install Docker Engine
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 🔧 Step 7 — Verify Docker Installation
```bash
sudo docker run hello-world
```

## 🔧 Step 8 — Allow Non-root Docker Usage
```bash
sudo usermod -aG docker $USER
```

## 🔧 Step 9 — Verify Docker Access
```bash
docker ps
```