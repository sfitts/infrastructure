# Jenkins Master
#
# Jenkins 1.565.1 (LTS)
#

FROM ubuntu:14.04
MAINTAINER Sean Fitts "smfitts@gmail.com"

# Install things we need either to install or when doing builds
RUN apt-get update && apt-get install -y wget git python python-dev

# Install PIP and virtualenv
RUN wget --no-check-certificate https://bootstrap.pypa.io/get-pip.py && python get-pip.py
RUN pip install virtualenv

# Add the ZeroMQ libraries
ADD libzmq /usr/local

# Install current LTS version of Jenkins
RUN echo deb http://pkg.jenkins-ci.org/debian-stable binary/ >> /etc/apt/sources.list
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
RUN apt-get update && apt-get install -y jenkins=1.565.1

# Create jenkins home and make a volume
RUN mkdir /jenkins; chmod 775 /jenkins; chown jenkins /jenkins
RUN mkdir /jenkins/.gradle; chmod 775 /jenkins/.gradle; chown jenkins /jenkins/.gradle
ADD gradle.properties /jenkins/.gradle/gradle.properties
# Preserve permissions -- see https://github.com/dotcloud/docker/issues/2969
RUN touch /jenkins/foo; chmod 666 /jenkins/foo
VOLUME ["/jenkins"]

# Configure jenkins home directory and set entrypoint
ENV HOME /jenkins
ENV GRADLE_USER_HOME /jenkins/.gradle
ENV JENKINS_HOME /jenkins
ENTRYPOINT exec su jenkins -c "java -jar /usr/share/jenkins/jenkins.war --httpPort=18080"
