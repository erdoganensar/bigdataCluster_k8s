FROM ubuntu:latest

USER root

# open port 22
EXPOSE 22

RUN apt-get update

# OpenJDK installation
RUN apt-get install -y openjdk-8-jre openjdk-8-jdk 
RUN apt-get install -y openssh-server  
RUN apt-get install -y vim nano curl
RUN apt-get install -y python3 python3-pip python-is-python3
RUN apt-get install -y telnet net-tools iputils-ping wget
RUN apt-get install -y netcat 
RUN apt-get install -y sshpass
# add hadoop user
RUN useradd -m -s /bin/bash hadoop



ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64


CMD ["/usr/sbin/sshd", "-D"]
