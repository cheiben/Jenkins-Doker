# Jenkins-Doker

1 .Building blueocean docker image

docker build -t myjenkins-blueocean:2.440.1-1 . 

## 2.440.1.1 version from Jenkins https://www.jenkins.io/doc/book/installing/docker/



2. Create Network jenkins

run command :
==> docker network create jenkins

==> docker network ls (to list netwok)

3. Run container on Windows

 docker run --name jenkins-blueocean --restart=on-failure --detach `
>>   --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
>>   --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
>>   --volume jenkins-data:/var/jenkins_home `
>>   --volume jenkins-docker-certs:/certs/client:ro `
>>   --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.440.1

or  Mac/linux

docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:xxxxx (version)


++++ run on cli : docker ps 

output : 

CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                                              NAMES
444a90968067   myjenkins-blueocean:2.440.1-1   "/usr/bin/tini -- /u…"   5 minutes ago   Up 5 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-blue

----Browsring to Jenkins-----
http://127.0.0.1:8080/login

We need to retrieve the login from : /var/jenkins_home/secrets/initialAdminPassword

Using Docker commands line 
run: 
==> docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword



 
