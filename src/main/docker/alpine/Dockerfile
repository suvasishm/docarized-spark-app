FROM openjdk:8-jdk-alpine

MAINTAINER Suvasish Mondal <suvasishmndl@gmail.com>

# Spark 2.1.1 with Hadoop 2.7
ENV SPARK_VERSION 2.1.1
ENV HADOOP_VERSION 2.7
ENV INSTALL_DIR /usr/local
ENV SPARK_HOME $INSTALL_DIR/spark_$SPARK_VERSION
ENV SPARK_TGZ_URL https://d3kbcqa49mib13.cloudfront.net/spark-2.1.1-bin-hadoop2.7.tgz

RUN apk update \
      && apk upgrade \
      && apk add --update bash \
      && apk add --update curl \
      && rm -rf /var/cache/apk/*

# Download and install Spark.
# Additionally, the Spark installation directory is renamed to 'spark_version' and the downloaded tarball is deleted.
WORKDIR $INSTALL_DIR
RUN set -x \
      && curl -fSL "$SPARK_TGZ_URL" -o spark.tgz \
      && tar -xzf spark.tgz \
      && mv spark-* spark_$SPARK_VERSION \
      && rm spark.tgz

# Define environment variables useful for deploying our Spark application in the Docker container.
ENV APP_HOME /opt/docker-spark-scala
ENV APP_VERSION 0.0.1
ENV APP_SCALA_VERSION 2.11
ENV APP_JAR dockerized-spark-app_$APP_SCALA_VERSION-$APP_VERSION.jar

# Deploy our Spark application in the Docker container.
# Finally, the command to be performed when the container is run is defined by the `ENTRYPOINT` instruction,
# which executes the Spark application in the local mode using two cores.
WORKDIR $APP_HOME
ADD deploy $APP_HOME
ENTRYPOINT "$SPARK_HOME/bin/spark-submit" --class SimpleApp --master local[4] "$APP_JAR"