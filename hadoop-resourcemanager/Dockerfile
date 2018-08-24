# AMEE hadoop resourcemanager
# License: GPL-3.0

FROM amee/hadoop-base:latest
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:8088/ || exit 1

ADD hadoop-resourcemanager-run.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hadoop-resourcemanager-run.sh

EXPOSE 8088

WORKDIR "/opt/amee/scripts/"
CMD ["./hadoop-resourcemanager-run.sh"]
