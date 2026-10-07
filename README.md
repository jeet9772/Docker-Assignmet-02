# Docker Assignment 2

## Objective

Create a Docker image using the **Ubuntu latest** image, install Node.js, npm and `http-server`, and run a simple HTML webpage inside a Docker container.

---

## Folder Structure

```text
docker-assignment-02/
├── Dockerfile
├── README.md
└── hello-docker/
    └── index.html
```

---

## Step 1: Create Dockerfile

The Dockerfile uses Ubuntu latest and installs the required packages.

```dockerfile
FROM ubuntu:latest

MAINTAINER Jeetendra Singh

RUN apt-get update

RUN apt-get install -y nodejs

RUN apt-get install -y npm

RUN npm install -g http-server

RUN if [ ! -e /usr/bin/node ]; then ln -s /usr/bin/nodejs /usr/bin/node; fi

COPY hello-docker/index.html /usr/apps/hello-docker/index.html

WORKDIR /usr/apps/hello-docker/

CMD ["http-server", "-s"]
```

---

## Step 2: Create Test HTML Page

File:

```text
hello-docker/index.html
```

Content:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Jeetendra Docker Web</title>
</head>
<body>
    <h1>Hello from Jeetendra</h1>
    <p>This webpage is running inside a Docker container.</p>
</body>
</html>
```

---

## Step 3: Build Docker Image

Build and tag the image:

```bash
docker build -t jeetendra:docker-web .
```

Check the image:

```bash
docker images
```

---

## Step 4: Run Docker Container

Run the container and map host port `8080` to container port `8080`:

```bash
docker run -d --name jeetendra-web -p 8080:8080 jeetendra:docker-web
```

Check the running container:

```bash
docker ps
```

Expected port mapping:

```text
0.0.0.0:8080->8080/tcp
```

---

## Step 5: Access the Webpage

Open the following URL in a browser:

```text
http://<VM-IP>:8080/index.html
```

Example:

```text
http://13.207.26.237:8080/index.html
```

---

## Step 6: Expected Output

The webpage displays:

```text
Hello from Jeetendra

This webpage is running inside a Docker container.
```

The webpage was successfully tested from the browser.

---

## Step 7: Verify from Terminal

The webpage can also be tested using:

```bash
curl http://localhost:8080/index.html
```

Expected output contains:

```html
<h1>Hello from Jeetendra</h1>
<p>This webpage is running inside a Docker container.</p>
```

---

## Step 8: Cleanup

After testing, stop and remove the container:

```bash
docker stop jeetendra-web
docker rm jeetendra-web
```

Remove the Docker image:

```bash
docker rmi jeetendra:docker-web
```

Verify:

```bash
docker ps -a
docker images
```

The custom container and image should no longer be present.

---

## Technologies Used

- Docker
- Ubuntu
- Node.js
- npm
- http-server
- HTML

---

## Assignment Status

**Docker Assignment 2 - Completed Successfully ✅**
