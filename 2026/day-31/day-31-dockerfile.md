# Day 31 -- Dockerfile: Build Your Own Images

------------------------------------------------------------------------

# Task 1 -- Your First Dockerfile

Create a folder:

``` text
my-first-image/
```

Create a **Dockerfile**:

``` dockerfile
FROM ubuntu

RUN apt update && apt install -y curl

CMD ["echo","Hello from my custom image!"]
```

## Build

``` bash
docker build -t my-ubuntu:v1 .
```

## Run

``` bash
docker run my-ubuntu:v1
```

Expected Output

``` text
Hello from my custom image!
```

------------------------------------------------------------------------

# Task 2 -- Dockerfile Instructions

Example Dockerfile

``` dockerfile
FROM nginx:alpine

WORKDIR /app

COPY . .

RUN echo "Docker Image Created Successfully"

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```

## Dockerfile Instructions

  Instruction   Purpose
  ------------- ------------------------------------------------
  FROM          Base image
  WORKDIR       Sets working directory
  COPY          Copies files into image
  RUN           Executes commands during build
  EXPOSE        Documents application port
  CMD           Default command executed when container starts

Build

``` bash
docker build -t dockerfile-demo:v1 .
```

Run

``` bash
docker run -d -p 8080:80 dockerfile-demo:v1
```

------------------------------------------------------------------------

# Task 3 -- CMD vs ENTRYPOINT

## CMD

``` dockerfile
FROM ubuntu

CMD ["echo","Hello"]
```

Run

``` bash
docker run cmd-demo
```

Output

``` text
Hello
```

Override CMD

``` bash
docker run cmd-demo ls
```

Output

``` text
Runs ls instead of echo Hello
```

------------------------------------------------------------------------

## ENTRYPOINT

``` dockerfile
FROM ubuntu

ENTRYPOINT ["echo"]
```

Run

``` bash
docker run entrypoint-demo Hello Docker
```

Output

``` text
Hello Docker
```

### Difference

  CMD                 ENTRYPOINT
  ------------------- ---------------------------
  Default command     Fixed executable
  Can be replaced     Arguments are appended
  Used for defaults   Used for main application

------------------------------------------------------------------------

# Task 4 -- Build a Simple Website

Create

``` text
index.html
```

Example

``` html
<!DOCTYPE html>
<html>
<head>
<title>Docker</title>
</head>
<body>
<h1>Hello from Docker!</h1>
</body>
</html>
```

Dockerfile

``` dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/

EXPOSE 80
```

Build

``` bash
docker build -t my-website:v1 .
```

Run

``` bash
docker run -d --name my-website -p 8080:80 my-website:v1
```

Access

``` text
http://localhost:8080
```

or on AWS EC2

``` text
http://<EC2-Public-IP>:8080
```

------------------------------------------------------------------------

# Task 5 -- .dockerignore

Create

``` text
.dockerignore
```

Contents

``` text
node_modules
.git
*.md
.env
```

### Why use .dockerignore?

-   Faster builds
-   Smaller images
-   Better security
-   Prevents unnecessary files from being copied

------------------------------------------------------------------------

# Task 6 -- Build Optimization

Poor Dockerfile

``` dockerfile
COPY . .

RUN npm install
```

Optimized Dockerfile

``` dockerfile
COPY package*.json ./

RUN npm install

COPY . .
```

### Why is this better?

-   Docker caches dependency installation.
-   If only application code changes, dependencies are reused.
-   Builds become much faster.

View image layers

``` bash
docker image history my-website:v1
```

------------------------------------------------------------------------

# Useful Commands

``` bash
docker build -t image-name:v1 .

docker images

docker run image-name:v1

docker ps

docker ps -a

docker logs <container-name>

docker exec -it <container-name> sh

docker image history <image-name>

docker image inspect <image-name>
```

------------------------------------------------------------------------
