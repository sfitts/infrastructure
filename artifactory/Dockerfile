# Artifactory
#
# Version Artifactory-3.2.1.1
#

FROM ubuntu:14.04
MAINTAINER Sean Fitts "smfitts@gmail.com"

# Unzip is required until ADD supports zip files
RUN apt-get update && apt-get install -y openjdk-7-jre-headless unzip

# Download the current version of Artifactory
ADD http://dl.bintray.com/content/jfrog/artifactory/artifactory-3.2.1.1.zip?direct /tmp/artifactory.zip

# Create a volume to hold A
RUN mkdir /artifactory
RUN unzip /tmp/artifactory.zip -d /artifactory

VOLUME /artifactory
WORKDIR /artifactory
EXPOSE 8081

# Run the embedded tomcat container
ENTRYPOINT ["/bin/sh", "-c", "artifactory-*/bin/artifactory.sh"]
