# Installazione Jenkins in un container Docker [(dalla guida ufficiale per Windows)](https://www.jenkins.io/doc/book/installing/docker/#on-windows)

## Prerequisites

[Docker Desktop for Windows](https://docs.docker.com/desktop/windows/install/) installed.

### 1. Create a bridge network in Docker
`docker network create jenkins`

### 2. Run a docker:dind Docker image

`docker run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home docker:dind`

### 3. Customise official Jenkins Docker image by building the Dockerfile

`docker build -t myjenkins-blueocean:1.1 .`

### 4. Run your own myjenkins-blueocean:1.1 image as a container in Docker

`docker run --name jenkins-blueocean --rm --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:1.1`


