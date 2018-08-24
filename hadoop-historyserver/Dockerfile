# AMEE hadoop historyserver
# License: GPL-3.0

FROM amee/hadoop-base:latest
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:8188/ || exit 1

ENV YARN_CONF_yarn_timeline___service_leveldb___timeline___store_path=/hadoop/yarn/timeline
RUN mkdir -p /hadoop/yarn/timeline
VOLUME /hadoop/yarn/timeline

ADD hadoop-historyserver-run.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hadoop-historyserver-run.sh

EXPOSE 8188

WORKDIR "/opt/amee/scripts/"
CMD ["./hadoop-historyserver-run.sh"]
