# 🚀This documentation explains how to install Docker, set up a Docker Swarm cluster, and deploy **Portainer** for cluster management and Running a nginx Service with ingress.  

---
##  Prerequisites
- Ubuntu 24.04 (or similar Linux distribution)
- At least 2 nodes (1 manager, 1 worker)
- Root or sudo access

##  1. Remove Old Versions

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

## 2.Add Docker's official GPG key:

```bash
sudo apt-get update
```

```bash
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```
```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

## 3.Add the repository to Apt sources:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 4.Install Docker

```bash
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 5.configuration for join a node for lunch docker swarm

```bash
docker swarm init --advertise-addr $YOURMASTERIP(for example: 192.168.64.130)
```

## 6.join another node for  docker swarm

- after run docker swarm init command you give a command in terminal for join another node
- This command for example: ( in terminal) 

- docker swarm join --token SWMTKN-1-0okhu09mf3bra9utfdjup6wsoouwac0iajwm6tzo4qnklmtr2x-0damzrmu9e94zpg1z6x1a1f7n 192.168.64.130:2377(This is different for everyone)

## 7.check for available nodes 

```bash
docker node ls
```

## 8.Install Portainer for manage your docker swarm
```bash
curl -L https://downloads.portainer.io/ce-lts/portainer-agent-stack.yml -o portainer-agent-stack.yml
```
```bash
docker stack deploy -c portainer-agent-stack.yml portainer
```

<img width="1259" height="654" alt="image" src="https://github.com/user-attachments/assets/ec4a00dc-45c2-413f-bf1e-b264f61e8ba1" />

<img width="1259" height="657" alt="image" src="https://github.com/user-attachments/assets/60591bb8-9399-460b-a952-e1405269e289" />

## 9.Running a nginx Service with ingress in my docker swarm cluster

```bash
docker service create --name static-web --publish published=80,target=80 nginx:latest
```

- you must see your nginx app with all swarm ip for cluster

<img width="1215" height="654" alt="image" src="https://github.com/user-attachments/assets/acaa6c64-f4e7-4d86-bf11-434a1da13da8" />
