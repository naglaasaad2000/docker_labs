# ITI - Docker Lab 🐋

## Task 1: Working with Docker Hello-world Image
### Objective
Learn how to run a container using the hello-world image and manage containers and images.

### Steps
#### 1. Run a Container with hello-world Image
docker pull hello-world
docker run hello-world
#### 2. Check Container Status and Explain
docker ps -a
its statuse is exited that is because it designed to print a message and then exited
```
#### 3. Start the Stopped Container
docker run hello-world
```
#### 4. Remove the Container
docker rm jovial_carson
```
#### 5. Remove the Image
docker rmi hello-world
```
---

## Task 2: Running Container with Ubuntu Image
### Objective
Run an Ubuntu container in interactive mode, create a file inside it, and manage containers.

### Steps
#### 1. Run Ubuntu Container in Interactive Mode
docker run -it ubuntu
```
#### 2. Create a File inside the Container
touch new-docker
```
#### 3. Stop and Remove the Container
exit
docker ps -a
docker rm bold_bouman
#### 4. Check File Status
ls -l new-docker
```
#### 5. What happened to hello-docker file?
it is deleted because we stop and remove the container
```
#### 6. Remove All Stopped Containers
docker container prune
#### 7. Bonus: Remove All Containers in One Command
docker rm -f $(docker ps -a -q)
```

---
## Task 3: Creating a Custom Nginx Docker Image
### Objective
Create a custom Docker image using Nginx and a local HTML file.

### Steps
#### 1. Create a Local HTML File
touch index.html
```
#### 2. Write Dockerfile and Copy the HTML file to the Docker Image
vi Dockerfile
FROM nginx:alpine
COPY index.html /user/share/nginx/html/index.html
```
#### 3. Run Container with New Image
docker run -d -p 8080:80 nginx-naglaa_saad
```

#### 4. Test the Container, open your browser and navigate to http://localhost:8088 to check if everything is okay
it display my index.html
```

