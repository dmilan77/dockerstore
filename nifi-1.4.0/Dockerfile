FROM centos:7.3.1611
MAINTAINER Milan Das

RUN yum install -y wget vim curl unzip which

# Java Version
ENV JAVA_DOWNLOAD_URL http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm
ENV NIFI_HOME_DIR /opt/nifi-1.4.0
COPY nifi-1.4.0-bin.tar.gz /tmp/
COPY jdk-8u151-linux-x64.rpm /tmp/
# Download and unarchive Java
RUN mkdir -p /opt &&\
  rpm -ivh /tmp/jdk-8u151-linux-x64.rpm &&\
  tar -xvf /tmp/nifi-1.4.0-bin.tar.gz --directory /opt/ &&\
  useradd --shell /bin/bash nifi &&\
  chown -R nifi:nifi $NIFI_HOME_DIR 
  

USER nifi
WORKDIR $NIFI_HOME_DIR
#ENTRYPOINT [" service nifi start"]

#CMD ["service nifi start"]
ENTRYPOINT ["bin/nifi.sh"]
CMD ["run"]
