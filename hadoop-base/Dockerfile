# AMEE hadoop base image
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

# Hadoop
RUN curl -s https://archive.apache.org/dist/hadoop/core/hadoop-2.7.7/hadoop-2.7.7.tar.gz | tar xz -C /usr/local
RUN mv /usr/local/hadoop-2.7.7 /usr/local/hadoop

ENV HADOOP_PREFIX /usr/local/hadoop
ENV HADOOP_COMMON_HOME /usr/local/hadoop
ENV HADOOP_HDFS_HOME /usr/local/hadoop
ENV HADOOP_MAPRED_HOME /usr/local/hadoop
ENV HADOOP_YARN_HOME /usr/local/hadoop
ENV HADOOP_CONF_DIR /usr/local/hadoop/etc/hadoop
ENV YARN_CONF_DIR $HADOOP_PREFIX/etc/hadoop

ENV MULTIHOMED_NETWORK=1

ENV USER=root
ENV PATH=${PATH}:$HADOOP_PREFIX/bin

# Entrypoint
ADD hadoop-base-entrypoint.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hadoop-base-entrypoint.sh

WORKDIR "/opt/amee/scripts/"
ENTRYPOINT ["./hadoop-base-entrypoint.sh"]
