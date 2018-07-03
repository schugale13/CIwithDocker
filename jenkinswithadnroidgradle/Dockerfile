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

# Jenkins Settings, i.e. Maven, Gradle 
COPY config/hudson.plugins.gradle.Gradle.xml /usr/share/jenkins/ref/hudson.plugins.gradle.Gradle.xml

# tell Jenkins that no banner prompt for pipeline plugins is needed
# see: https://github.com/jenkinsci/docker#preinstalling-plugins
RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state


# Adding the specific config for Java with Maven APP
COPY jobs/helloWorldAndroid.xml /usr/share/jenkins/ref/jobs/helloWorldAndroid/config.xml


############################################
#Install Android SDK and needet stuff for building Android apps
############################################

USER root

# Install Android SDK
RUN cd /opt && \
	wget --output-document=android-sdk.tgz --quiet http://dl.google.com/android/android-sdk_r24.1.2-linux.tgz && \
	tar xzf android-sdk.tgz && \
	rm -f android-sdk.tgz && \
	chown -R root.root android-sdk-linux

# Setup environment
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

#Accept liceses
RUN mkdir /opt/android-sdk-linux/licenses
RUN echo 8933bad161af4178b1185d1a37fbf41ea5269c55 > /opt/android-sdk-linux/licenses/android-sdk-license
RUN echo d56f5187479451eabf01fb78af6dfcb131a6481e >> /opt/android-sdk-linux/licenses/android-sdk-license
RUN echo 84831b9409646a918e30573bab4c9c91346d8abd > /opt/android-sdk-linux/licenses/android-sdk-preview-license

RUN	android update sdk --no-ui && \
	android update sdk --all --filter sys-img-armeabi-v7a-android-23 --no-ui --force
