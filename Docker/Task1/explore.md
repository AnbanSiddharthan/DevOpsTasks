## Install docker on EC2 and explore the docker commands (docker images, containers, volumes, network)

### Instal Docker

```bash
sudo apt install docker.io -y
docker --version
```
### Start Docker

```bash
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```
### Allow Current User to Run Docker

```bash
sudo usermod -aG docker ubuntu
newgrp docker
docker ps
```
### Explore Docker Images

```bash
docker images
docker pull nginx
docker images
```

### Explore Containers

```bash
docker run -d --name webserver -p 80:80 nginx
docker ps
docker stop webserver
docker start webserver
docker restart webserver
docker logs webserver
docker exec -it webserver bash
docker rm -f webserver
```

### Explore Docker Volumes

```bash
docker volume create myvolume
docker volume ls
docker volume inspect myvolume

docker run -d \
--name volume-nginx \
-v myvolume:/usr/share/nginx/html \
-p 8080:80 nginx

docker volume ls
docker rm -f volume-nginx
docker volume rm myvolume
```

### Explore Docker Networks

```bash
docker network ls
docker network create mynetwork
docker network ls
docker network inspect mynetwork
docker run -d --name web1 --network mynetwork nginx
docker inspect web1
docker rm -f web1
docker network rm mynetwork
```

### Screenshots

<img width="1477" height="743" alt="image" src="https://github.com/user-attachments/assets/dd3a140f-988f-44a3-a803-aa9c7efba438" />

<img width="1477" height="747" alt="image" src="https://github.com/user-attachments/assets/0546f489-b3ce-427d-bd03-1c1aa9ae3357" />

<img width="1477" height="752" alt="image" src="https://github.com/user-attachments/assets/9edc675f-04af-4707-9fdb-8db2c1b7ca33" />

<img width="1478" height="751" alt="image" src="https://github.com/user-attachments/assets/5303e78c-c867-4f0d-86b3-f66e2dfd20a6" />

<img width="1482" height="751" alt="image" src="https://github.com/user-attachments/assets/bfef5a38-56b7-4326-93e9-90669705d80f" />

<img width="1487" height="747" alt="image" src="https://github.com/user-attachments/assets/8655e88c-f8d6-471c-b5c8-5ea9235a6394" />

<img width="1482" height="747" alt="image" src="https://github.com/user-attachments/assets/4128f80d-66dc-4fd7-9a4a-d866fed1a451" />

<img width="1477" height="745" alt="image" src="https://github.com/user-attachments/assets/5c03749c-7909-456c-b805-047a4ff1945a" />

<img width="1476" height="750" alt="image" src="https://github.com/user-attachments/assets/152bbc79-0894-471d-b524-fcc9d8634378" />

<img width="1482" height="733" alt="image" src="https://github.com/user-attachments/assets/db854aa6-56f7-4e58-aafa-7842f6510197" />
