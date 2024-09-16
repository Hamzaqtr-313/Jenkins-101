# Jenkins Interface from where you can create pipeline
![image](https://github.com/user-attachments/assets/22ccbce2-9ee8-4329-92a4-1bf26dce8b20)

# For managing pluggins and for using it with Kubernetes and Docker here is its interface
![image](https://github.com/user-attachments/assets/bec98d0d-632f-4ec9-95d9-87cf6b2d3f68)

# For Creating Pipeline we have this interface
![image](https://github.com/user-attachments/assets/d8e04751-1fb9-49a7-bc0f-9d72e1e5b0d3)

# Installation
## Build the Jenkins BlueOcean Docker Image
```
docker build -t myjenkins-blueocean:2.414.2 .

```

## Create the network 'jenkins'
```
docker network create jenkins
```

## Run the Container
### Windows
```
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.414.2
```


## Get the Password
```
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

## Connect to the Jenkins
```
https://localhost:8080/
```

## Installation Reference:
https://www.jenkins.io/doc/book/installing/docker/

https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
docker inspect <container_id> | grep IPAddress
```

## Using Jenkins Python Agent
```
docker pull hamza313/myjenkinsagents:python
```
