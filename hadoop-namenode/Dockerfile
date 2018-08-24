# AMEE hadoop namenode
# License: GPL-3.0

FROM amee/hadoop-base:latest
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:50070/ || exit 1

ENV HDFS_CONF_dfs_namenode_name_dir=file:///hadoop/dfs/name
RUN mkdir -p /hadoop/dfs/name
VOLUME /hadoop/dfs/name

ADD hadoop-namenode-run.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hadoop-namenode-run.sh

EXPOSE 50070

WORKDIR "/opt/amee/scripts/"
CMD ["./hadoop-namenode-run.sh"]
