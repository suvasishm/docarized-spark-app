# A Simple Spark application on Docker (dockerized spark-on-scala)

a) The project contains a simple Spark project written on Scala (https://github.com/suvasishm/spark-on-scala).

b) The above project has been dockerized on alpine & ubuntu linux platform to run on respective docker containers.

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


##### Copy the package to the deploy directory. /deploy will be served as context in the following steps 
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

