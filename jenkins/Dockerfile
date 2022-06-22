FROM jenkins/jenkins:latest

LABEL maintainer "Dimuthu Daundasekara <dimuit86@gmail.com>"

# set variables - *** CHANGE ME ***
ARG timezone="America/New_York"
ENV TIMEZONE $timezone

# switch to install packages via apt
USER root

# update and install common packages
RUN set +x \
  && env \
  && apt-get update \
  && apt-get -y upgrade \
  && apt-get -y install openrc openntpd tzdata python3 python3-pip jq git wget zip curl

# update and install Docker CE and associated packages
RUN set +x \
  && apt-get install -y \
     lsb-release software-properties-common \
     apt-transport-https ca-certificates curl gnupg2 \
  && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
  && add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable" \
  && apt-get update \
  && apt-get -y upgrade \
  && apt-get install -y docker-ce \
  && systemctl enable docker

# set permissions for jenkins user
RUN set +x \
    && usermod -aG staff,docker jenkins \
  && exec bash

# Install NodeJS
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get install -y nodejs

# install jenkins plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

RUN set +x \
  && apt-get clean

# set timezone to America/New_York
RUN set +x \
  && cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
  && echo "America/New_York" >  /etc/timezone \
  && date


ENV JAVA_OPTS_DISABLE_WIZARD="-Djenkins.install.runSetupWizard=false"

RUN wget -O /var/sonar-scanner-cli-4.7.0.2747-linux.zip  https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.7.0.2747-linux.zip
RUN unzip /var/sonar-scanner-cli-4.7.0.2747-linux.zip -d /var/jenkins_home/

USER jenkins

