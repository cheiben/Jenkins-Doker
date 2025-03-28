# Jenkins-Docker Setup Guide

This guide walks through setting up Jenkins with Docker using the Blue Ocean interface.

## Prerequisites

- Docker installed on your system
- Basic knowledge of Docker commands

## 1. Building the Jenkins Blue Ocean Docker Image

Build the custom Jenkins Blue Ocean image:

```bash
docker build -t myjenkins-blueocean:2.440.1-1 .
```

> Note: Version 2.440.1-1 comes from the official [Jenkins Docker installation guide](https://www.jenkins.io/doc/book/installing/docker/).

## 2. Create Jenkins Network

Create a dedicated Docker network for Jenkins:

```bash
docker network create jenkins
```

Verify the network was created:

```bash
docker network ls
```

## 3. Run Jenkins Container

### Windows PowerShell

```powershell
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.440.1-1
```

### macOS/Linux

```bash
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.440.1-1
```

### Verify Container is Running

```bash
docker ps
```

Expected output:
```
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                                              NAMES
444a90968067   myjenkins-blueocean:2.440.1-1   "/usr/bin/tini -- /u…"   5 minutes ago   Up 5 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-blueocean
```

## 4. Accessing Jenkins

1. Navigate to the Jenkins web interface:
   ```
   http://127.0.0.1:8080/login
   ```

2. Retrieve the initial admin password:
   ```bash
   docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
   ```

3. Copy the displayed password and paste it into the Jenkins setup wizard to continue with configuration.

## Next Steps

- Install recommended plugins
- Create your first admin user
- Configure your Jenkins instance

## Troubleshooting

If Jenkins doesn't start properly, check the logs:
```bash
docker logs jenkins-blueocean
```


 by#Cheikh B
