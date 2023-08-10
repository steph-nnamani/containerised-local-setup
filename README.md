Project prerequisites:
1. Docker daemon/engine must be installed in your locan environment.


version: '3.8'
services:
  jenkins:
    container_name: jenkins
    image: jenkins/jenkins
    ports:
      - "8080:8080"
    volumes:
      - "$PWD/jenkins-home:/var/jenkins_home"
    networks:
      - net
networks:
  net:


In this Docker Compose configuration:

The version is specified as 3.8, which indicates the version of Docker Compose to use. You can use the appropriate version based on your Docker Compose installation.

Under the services section, there is a service named jenkins, which represents the Jenkins container.

The container_name specifies the custom name for the Jenkins container as jenkins.

The image setting defines the Docker image to use, and it's set to jenkins/jenkins, which is the official Jenkins image from Docker Hub.

By default, jenkins runs on tomcat, and therefore expose port 8080 by default.
The ports setting maps port 8080 on the host to port 8080 on the container, allowing you to access Jenkins web interface on http://localhost:8080.  Also expose port 50000 which is the port that jenkins master communicates with jenkins slave

The volumes setting mounts the $PWD/jenkins-home directory on the host to /var/jenkins_home inside the container. This provides data persistence for Jenkins configurations and data.

The networks setting specifies that the Jenkins container should be connected to the net network.

Lastly, the networks section defines a network named net, which the Jenkins container will be connected to.

Run below command in your project home directory.
docker-compose up 

We will run the container with the following commandin detached mode so it runs in the background.

docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins

Make sure you are in the directory where the docker-compose.yml file is located when running the docker-compose command. This will start Jenkins in detached mode (-d), and you can access the Jenkins web interface at http://localhost:8080.


docker ps 
docker logs <container-id>

credential scopes:
  System: only available on jenkins server and and NOT for jenkins jobs
  Global: everywhere accessible 

File Structure
==============
containerised-local-lab-setup:
  jenkins-home: #this is an empty directory referenced in the docker-compose file.
  docker-compose.yml
  Dockerfile
  jenkins.yaml