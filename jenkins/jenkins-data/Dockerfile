FROM debian:jessie
MAINTAINER Luis Carlin <luiscarlin@gmail.com>

# Create the jenkins user with same UID as in jenkins image
RUN useradd -d "/var/jenkins_home" -u 1000 -m -s /bin/bash jenkins

# Create logs folder
RUN mkdir -p /var/log/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins

# Make the log folder a mount and jenkins home
VOLUME ["/var/log/jenkins", "/var/jenkins_home"]

# Set Jenkins as the user opf this container
USER jenkins

# Output the purpose of this container
CMD ["echo", "Data container for Jenkins"]
