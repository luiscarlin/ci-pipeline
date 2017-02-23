FROM jenkins:1.609.1
MAINTAINER Luis Carlin <luiscarlin@gmail.com>

USER root
RUN mkdir /var/log/jenkins
RUN mkdir /var/cache/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins
USER jenkins

# 1 GB memory
ENV JAVA_OPTS="-Xmx1024m"

# base and max pool of handlers, logs folder location, and jenkins.war location
ENV JENKINS_OPTS="--handlerCountStartup=100 --handlerCountMax=300 --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war"
