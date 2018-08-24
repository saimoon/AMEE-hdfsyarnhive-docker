# AMEE hive
# License: GPL-3.0

FROM amee/hadoop-base:latest
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

ENV HIVE_VERSION 2.3.3

ENV HIVE_HOME /usr/local/hive
ENV PATH $HIVE_HOME/bin:$PATH
ENV HADOOP_HOME $HADOOP_PREFIX

WORKDIR "/opt/amee/scripts/"

# Hive
# Downloading hive tgz is pretty slow, so for test/dev purpose we'll get it from FS
# In production, remember to use curl command
COPY apache-hive-2.3.3-bin.tar.gz .
RUN tar xvf ./apache-hive-2.3.3-bin.tar.gz -C /usr/local
#RUN curl -s http://apache.panu.it/hive/hive-2.3.3/apache-hive-2.3.3-bin.tar.gz | tar xz -C /usr/local
RUN mv /usr/local/apache-hive-2.3.3-bin /usr/local/hive

# PostgreSQL JDBC
RUN curl -s -o $HIVE_HOME/lib/postgresql-jdbc.jar https://jdbc.postgresql.org/download/postgresql-9.4.1212.jar

#Spark should be compiled with Hive to be able to use it
#hive-site.xml should be copied to $SPARK_HOME/conf folder

#Custom configuration goes here
ADD conf/hive-site.xml $HIVE_HOME/conf
ADD conf/beeline-log4j2.properties $HIVE_HOME/conf
ADD conf/hive-env.sh $HIVE_HOME/conf
ADD conf/hive-exec-log4j2.properties $HIVE_HOME/conf
ADD conf/hive-log4j2.properties $HIVE_HOME/conf
ADD conf/ivysettings.xml $HIVE_HOME/conf
ADD conf/llap-daemon-log4j2.properties $HIVE_HOME/conf

ADD hive-entrypoint.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hive-entrypoint.sh

ADD hive-startup.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hive-startup.sh

EXPOSE 10000
EXPOSE 10002

WORKDIR "/opt/amee/scripts/"
ENTRYPOINT ["./hive-entrypoint.sh"]
CMD ["./hive-startup.sh"]
