# 🚀 Docker Swarm + Portainer Setup Guide and Launch an Nginx Service with Ingress

This documentation explains how to install Docker, set up a Docker Swarm cluster, and deploy **Portainer** for cluster management.  

---
## 🚀 Prerequisites
- Ubuntu 24.04 (or similar Linux distribution)
- At least 2 nodes (1 manager, 1 worker)
- Root or sudo access

## 📌 1. Remove Old Versions & Install Docker (Official Package)

First, check for existing Docker/Container runtimes and remove them:

```bash
sudo apt update

for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do 
  sudo apt-get remove $pkg; 
done
---

---
Add Docker’s official GPG key:

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
---
