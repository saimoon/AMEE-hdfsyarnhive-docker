# AMEE hadoop nodemanager
# License: GPL-3.0

FROM amee/hadoop-base:latest
MAINTAINER Simome Rotondo <simone.rotondo@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:8042/ || exit 1

ADD hadoop-nodemanager-run.sh /opt/amee/scripts/
RUN chmod a+x /opt/amee/scripts/hadoop-nodemanager-run.sh

EXPOSE 8042

WORKDIR "/opt/amee/scripts/"
CMD ["./hadoop-nodemanager-run.sh"]
