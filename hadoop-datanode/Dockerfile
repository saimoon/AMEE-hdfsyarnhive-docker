# AMEE hadoop datanode
# License: GPL-3.0

FROM amee/hadoop-base:latest
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:50075/ || exit 1

ENV HDFS_CONF_dfs_datanode_data_dir=file:///hadoop/dfs/data
RUN mkdir -p /hadoop/dfs/data
VOLUME /hadoop/dfs/data

ADD hadoop-datanode-run.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hadoop-datanode-run.sh

EXPOSE 50075

WORKDIR "/opt/amee/scripts/"
CMD ["./hadoop-datanode-run.sh"]
