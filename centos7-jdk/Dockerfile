FROM centos:7.3.1611
MAINTAINER Milan Das

RUN yum install -y wget vim curl unzip which

# Java Version
ENV JAVA_DOWNLOAD_URL http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm

# Download and unarchive Java
RUN mkdir -p /opt &&\
  curl -jkLH "Cookie: oraclelicense=accept-securebackup-cookie" -o /tmp/java.rpm\
  ${JAVA_DOWNLOAD_URL} &&\
  rpm -ivh /tmp/java.rpm

# Setup SSH as it's a common requirement for downstream images
RUN yum install -y openssh && \
  ssh-keygen -f ~/.ssh/id_rsa -t rsa -q -N "" && \
  cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
  ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key && \
  ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key && \
  ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key && \
  ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key && \
  cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
  rm -rf /tmp

# Set environment
ENV JAVA_HOME /opt/${JAVA_PACKAGE}
ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/usr/lib64:/usr/glibc-compat/lib:
ENV PATH ${PATH}:${JAVA_HOME}/bin

