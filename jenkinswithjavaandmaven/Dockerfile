FROM jenkins/jenkins:lts
MAINTAINER Alexander Schug <alexander.schug@jipp.it>

USER root
RUN apt-get update \
      && apt-get install -y sudo curl\
      && apt-get install -y libltdl7\
      && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins

# installing specific list of plugins. see: https://github.com/jenkinsci/docker#preinstalling-plugins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/plugins.txt


############################################
# Configure Jenkins
############################################

# Jenkins defaut settings
COPY config/config.xml /usr/share/jenkins/ref/config.xml

# Jenkins Settings, i.e. Maven, 
COPY config/hudson.tasks.Maven.xml /usr/share/jenkins/ref/hudson.tasks.Maven.xml

# tell Jenkins that no banner prompt for pipeline plugins is needed
# see: https://github.com/jenkinsci/docker#preinstalling-plugins
RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state


# Adding the specific config for Java with Maven APP
COPY jobs/helloWorld.xml /usr/share/jenkins/ref/jobs/HelloWorld/config.xml