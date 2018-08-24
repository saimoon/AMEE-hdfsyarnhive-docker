# AMEE spark base image
# License: GPL-3.0

FROM phusion/baseimage:0.10.1
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

# Set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

WORKDIR /root

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Install prerequisites
RUN apt update && \
    apt install -y vim sudo curl wget openjdk-8-jre-headless netcat-openbsd

# Clean up APT when done
RUN apt clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Create fs structure
RUN bash -c 'mkdir -pv /opt/amee/scripts'

# Configure JAVA
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV PATH=${PATH}:/usr/lib/jvm/java-8-openjdk-amd64/bin

# Spark
ENV SPARK_VERSION=2.3.1
ENV HADOOP_VERSION=2.7

RUN curl -s https://archive.apache.org/dist/spark/spark-2.3.1/spark-2.3.1-bin-hadoop2.7.tgz | tar xz -C /usr/local
RUN mv /usr/local/spark-2.3.1-bin-hadoop2.7 /usr/local/spark

RUN apt install -y python3 python3-setuptools python3-pip

# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1

#ENV USER=root
#ENV PATH=${PATH}:$HADOOP_PREFIX/bin
