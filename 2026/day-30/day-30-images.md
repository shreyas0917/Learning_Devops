# Day 30 -- Docker Images & Container Lifecycle

## 1. Docker Images

### What is a Docker Image?

A Docker Image is a **read-only template** used to create containers.

**Remember** - Image = Blueprint - Container = Running Instance

### Pull Images

``` bash
docker pull nginx
docker pull ubuntu
docker pull alpine
```

### List Images

``` bash
docker images
```

### Ubuntu vs Alpine

  Ubuntu          Alpine
  --------------- ------------------
  Large           Very Small
  Many packages   Minimal packages
  Development     Production

### Inspect an Image

``` bash
docker image inspect nginx
```

### Remove an Image

``` bash
docker rmi ubuntu
```

------------------------------------------------------------------------

## 2. Image Layers

``` bash
docker image history nginx
```

Each Dockerfile instruction creates a read-only layer.

Example Dockerfile:

``` dockerfile
FROM python:3.14
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 80
CMD ["python","run.py"]
```

------------------------------------------------------------------------

## 3. Container Lifecycle

``` bash
docker create --name flask-container flask-app
docker start flask-container
docker pause flask-container
docker unpause flask-container
docker stop flask-container
docker restart flask-container
docker kill flask-container
docker rm flask-container
```

Check:

``` bash
docker ps -a
```

------------------------------------------------------------------------

## 4. Flask App ECS Practice

### Build Image

``` bash
docker build -t flask-app .
```

### Verify Image

``` bash
docker images
```

### Run Container

``` bash
docker run -d --name flask-container -p 8080:80 flask-app
```

### Check Running Container

``` bash
docker ps
```

### View Logs

``` bash
docker logs flask-container
docker logs -f flask-container
```

### Execute Inside Container

``` bash
docker exec -it flask-container sh
```

Run a single command:

``` bash
docker exec flask-container ls
docker exec flask-container pwd
```

### Inspect Container

``` bash
docker inspect flask-container
```

### Access Application

``` text
http://<EC2-Public-IP>:8080
```

Health endpoint:

``` text
http://<EC2-Public-IP>:8080/health
```

------------------------------------------------------------------------

## 5. Cleanup

``` bash
docker container prune
docker image prune -a
docker system df
docker system prune
```

------------------------------------------------------------------------
