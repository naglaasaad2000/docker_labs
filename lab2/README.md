# ITI - Docker Lab2 🐋

## Task 1:
Run a container using nginx image, and mount a directory from your host into the 
Docker container. example: /home/samy/nginx:/home/nginx (bind mount)

#### 1. Create Bind Mount Directory
```bash
mkdir nginx_bind_mount
cd nginx_bind_mount
pwd
```
### 2. Run a container using nginx image
```bash
docker run -d --name nginx_bind_mount -v /root/nginx_bind_mount:/user/share/nginx/html nginx
docker exec -it nginx_bind_mount bash
```
### 3. Echo any content to show when curl ip-address
```bash
cd /user/share/nginx/html
echo "Hello from Bind mount nginx" > index.html
exit
docker inspect -f '{{.NetworkSettings.IPAddress}}' nginx_bind_mount    ->172.17.0.2
curl 172.17.0.2

```

## Task 2:
### Steps
#### 1. Create 2 docker network (net-1 & net-2)
```bash
docker network create net-1
docker network create net-2
```
#### 2. Run 2 new containers using nginx:alpine image, and attach the net-1 to them
```bash
docker run -d --name nginx_net1 --net net-1 nginx:alpine
docker run -d --name nginx_net2 --network net-1 nginx:alpine

```
#### 3.  Run another 1 new containers using nginx:alpine image, and attach the net-2 to them
```bash
docker run -d --name nginx_net3 --net net-2 nginx:alpine
```
#### 4. Inspect the 3 containers to know their IPs and write them aside
```bash
docker inspect -f '{{.NetworkSettings.Networks.net-1.IPAddress}}' nginx_net1
172.18.0.2

docker inspect -f '{{.NetworkSettings.Networks.net-1.IPAddress}}' nginx_net2
172.18.0.3

docker inspect -f '{{.NetworkSettings.Networks.net-2.IPAddress}}' nginx_net3
172.20.0.2
can use : docker inspect nginx_net1 | grep IPAddress
```
#### 5. Enter a container in the net-1 network and try to ping a container in the net-2 
network (What do you notice?)
```bash
docker exec -it nginx_net1 sh 
Use ping or curl
ping 172.20.0.2
ping fails, because the two containers exist in different networks .
```
#### 6. Enter a container in the net-1 network and try to ping the other container in the 
same network (What do you notice?)
```bash
docker exec -it nginx_net1 sh 
curl 172.18.0.2
ping 172.18.0.3
ping successful and return response, because the two containers exist in the same network.
```
---
## Task 3: Explain the difference between Docker volumes and Bind Mount.
```bash
Bind mounts directly link a directory or file from the host to the container, ideal for development or scenarios requiring direct host access with low overhead.

Docker volumes, managed by Docker, offer portability and features like data management, suited for production environments needing data persistence and shared storage.
```


