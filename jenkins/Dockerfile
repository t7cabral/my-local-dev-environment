FROM jenkins/jenkins:lts
# FROM jenkins/jenkins:2.330-jdk11

ARG ADMIN_PASSWORD

ENV JENKINS_HOME /var/jenkins_home

# Install the custom plugins
#COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
#RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Create the admin account in jenkins
ENV JENKINS_OPTS \
    --argumentsRealm.passwd.admin=${ADMIN_PASSWORD} \
    --argumentsRealm.roles.user=admin \
    --argumentsRealm.roles.admin=admin \
    -Djenkins.install.runSetupWizard=false

# Install docker, unfortunately it's not in the debian repositories, so we need to add a repository
USER root

# Install some prerequisites
RUN apt-get update && \
    apt-get install -y \
    software-properties-common \
    apt-transport-https \
    ca-certificates \
    curl \
    sudo \
    gnupg2

# RUN apt-get install -y python3-pip \
#    && pipx install virtualenv

# Install the repository
#RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
#     add-apt-repository \
#     "deb [arch=amd64] https://download.docker.com/linux/debian \
#     $(lsb_release -cs) \
#     stable"


# Update and install docker
#RUN apt-get update && \
#     apt-get install -y docker-ce

# Now we need to allow jenkins to run docker commands! (This is not elegant, but at least it's semi-portable...)

## allowing jenkins user to run docker without specifying a password
RUN echo "jenkins ALL=(ALL) NOPASSWD: /usr/bin/docker" >> /etc/sudoers

# Create our alias file that allows us to use docker as sudo without writing sudo
#COPY docker_sudo_overwrite.sh /usr/local/bin/docker
#RUN chmod +x /usr/local/bin/docker

# switch back to the jenkins-user
USER jenkins

WORKDIR $JENKINS_HOME
