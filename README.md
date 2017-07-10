# A Simple Spark application written in Scala to run on Docker (dockerized spark-on-scala)

a) The project contains a simple Spark application written on Scala (https://github.com/suvasishm/spark-on-scala).

b) The above application has been dockerized for it to be able to run on docker container. 
Two docker containers has been written:-

 i) Based on Alpine. Find the image at https://hub.docker.com/r/suvasishm/dockerized-spark-app-on-alpine/
 
 ii) Based on Ubuntu. Find the image at https://hub.docker.com/r/suvasishm/dockerized-spark-app-on-ubuntu/

#### Pre-requisite

- Java 8
- SBT 0.13.15
- Docker 17.06.0-ce

#### Directory structure:

docker-spark-scala

    - /src
        - /docker
            - /alpine
                - /Dockerfile
            - /deploy
                - /dockerized-spark-app_2.11-0.0.1
            - /ubuntu
        - /scala
            - /SimpleApp
    - /build.sbt
    - README


##### Build package
$ cd /path/to/docker-spark-scala

$ sbt package


##### Copy the application jar to the deploy directory. This directory will be used as context in the following steps 
$ cp target/scala-2.11/dockerized-spark-app_2.11-0.0.1.jar src/main/docker/deploy/

$ cd src/main/docker/

##### Build the docker image
$ docker build -f alpine/Dockerfile -t dockerized-spark-app-on-alpine .

##### or,

$ docker build -f ubuntu/Dockerfile -t dockerized-spark-app-on-ubuntu .

##### Run the image
$ docker run -it --rm dockerized-spark-app-on-alpine

##### or,

$ docker run -it --rm dockerized-spark-app-on-ubuntu

