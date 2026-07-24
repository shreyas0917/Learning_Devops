# Day 32 -- Docker Volumes & Networking (Simple Revision Notes)

> **Goal:** Understand Docker Volumes and Networking in simple language.

------------------------------------------------------------------------

# Memory Trick

Think of Docker like a **Hotel**.

-   **Container = Hotel Room 🏨**
-   **Volume = Locker 🔒**
-   **Bind Mount = Shared Folder 📂**
-   **Network = Society 🏢**

Remember this and Day 32 becomes easy.

------------------------------------------------------------------------

# Task 1 -- Containers are Ephemeral

## What does Ephemeral mean?

**Ephemeral = Temporary**

Imagine you stay in a hotel room.

-   You keep your clothes inside.
-   You check out.
-   Hotel cleans the room.
-   Everything inside is gone.

Docker container works exactly the same.

## Run PostgreSQL

``` bash
docker run -d --name postgres-db -e POSTGRES_PASSWORD=admin -p 5432:5432 postgres:16
```

Enter PostgreSQL:

``` bash
docker exec -it postgres-db psql -U postgres
```

Create database:

``` sql
CREATE DATABASE dockerdemo;
```

Connect:

``` sql
\c dockerdemo
```

Create table:

``` sql
CREATE TABLE students(id SERIAL PRIMARY KEY,name VARCHAR(50));
```

Insert data:

``` sql
INSERT INTO students(name) VALUES('Shreyas');
```

Verify:

``` sql
SELECT * FROM students;
```

Delete container:

``` bash
docker stop postgres-db
```

``` bash
docker rm postgres-db
```

### Result

❌ Database gone

❌ Table gone

❌ Data gone

### Why?

Because data was stored **inside the container**.

------------------------------------------------------------------------

# Task 2 -- Named Volume

## Memory Trick

**Named Volume = Locker**

Room can be destroyed.

Locker still keeps your luggage.

    Container
        |
        v
    Named Volume

Create volume:

``` bash
docker volume create postgres-data
```

Run PostgreSQL:

``` bash
docker run -d --name postgres-db -e POSTGRES_PASSWORD=admin -v postgres-data:/var/lib/postgresql/data -p 5432:5432 postgres:16
```

Check volumes:

``` bash
docker volume ls
```

Inspect volume:

``` bash
docker volume inspect postgres-data
```

Delete container.

Create another one using the same volume.

### Result

✅ Data is still there.

### Remember

Container dies.

Volume survives.

------------------------------------------------------------------------

# Task 3 -- Bind Mount

## Memory Trick

**Bind Mount = Shared Folder**

Host folder:

    mywebsite
        |
        └── index.html

Create folder:

``` bash
mkdir ~/mywebsite
```

Go inside:

``` bash
cd ~/mywebsite
```

Create HTML:

``` bash
vim index.html
```

Run Nginx:

``` bash
docker run -d --name bind-nginx -p 8082:80 -v ~/mywebsite:/usr/share/nginx/html nginx
```

Edit file again:

``` bash
vim index.html
```

Refresh browser.

✅ Changes appear instantly.

### Why?

Both host and container are using the **same folder**.

------------------------------------------------------------------------

# Named Volume vs Bind Mount

  Named Volume        Bind Mount
  ------------------- ---------------
  Docker manages it   You manage it
  Best for Database   Best for Code
  Safe                Flexible

Easy Trick:

**Database → Volume**

**Code → Bind Mount**

------------------------------------------------------------------------

# Task 4 -- Docker Networking

## Memory Trick

Docker Network = Society

    Ubuntu
         |
         |
    PostgreSQL

If both are in the same society (network),

they can talk.

List networks:

``` bash
docker network ls
```

Inspect bridge:

``` bash
docker network inspect bridge
```

Find IP:

``` bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' postgres-db
```

Run Ubuntu:

``` bash
docker run -it --name ubuntu-test ubuntu bash
```

Install ping:

``` bash
apt update
```

``` bash
apt install iputils-ping -y
```

Ping PostgreSQL:

``` bash
ping 172.17.0.5
```

### Result

✅ Containers communicate using IP.

------------------------------------------------------------------------

# Task 5 -- Custom Bridge Network

Create network:

``` bash
docker network create my-app-net
```

Run PostgreSQL:

``` bash
docker run -d --name postgres-db --network my-app-net -e POSTGRES_PASSWORD=admin -v postgres-data:/var/lib/postgresql/data postgres:16
```

Run Ubuntu:

``` bash
docker run -it --name ubuntu-test --network my-app-net ubuntu bash
```

Ping by name:

``` bash
ping postgres-db
```

### Why does it work?

Docker has its own phonebook (DNS).

You remember:

    postgres-db

Docker remembers:

    172.x.x.x

------------------------------------------------------------------------

# Default Bridge vs Custom Bridge

  Default Bridge      Custom Bridge
  ------------------- ---------------
  Use IP              Use Name
  Docker creates it   You create it
  Basic testing       Real projects

Easy Trick:

**Default Bridge = IP**

**Custom Bridge = Name**

------------------------------------------------------------------------

# Task 6 -- Put Everything Together

1.  Create custom network.
2.  Create named volume.
3.  Run PostgreSQL on the custom network.
4.  Run another container on the same network.
5.  Ping using:

``` bash
ping postgres-db
```

If ping works,

✅ Networking is working.

------------------------------------------------------------------------

# Important Commands

``` bash
docker volume create postgres-data
docker volume ls
docker volume inspect postgres-data
docker network ls
docker network inspect bridge
docker network create my-app-net
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' postgres-db
```

------------------------------------------------------------------------

# Interview Questions

**What is a Container?**

A temporary running instance of an image.

**What is a Volume?**

Persistent storage that survives container deletion.

**What is a Bind Mount?**

A host folder shared with a container.

**What is Docker Network?**

A way for containers to communicate.

**Default Bridge?**

Containers communicate mainly using IP addresses.

**Custom Bridge?**

Containers communicate using names because Docker provides DNS.

------------------------------------------------------------------------

# One Minute Revision

-   Container = Hotel Room 🏨
-   Volume = Locker 🔒
-   Bind Mount = Shared Folder 📂
-   Network = Society 🏢
-   Default Bridge = IP
-   Custom Bridge = Name
-   Volume = Database
-   Bind Mount = Source Code

------------------------------------------------------------------------

# Revision Checklist

-   [ ] Ephemeral Container
-   [ ] Named Volume
-   [ ] Bind Mount
-   [ ] Docker Network
-   [ ] Default Bridge
-   [ ] Custom Bridge
-   [ ] Docker DNS
-   [ ] Ping by IP
-   [ ] Ping by Name
