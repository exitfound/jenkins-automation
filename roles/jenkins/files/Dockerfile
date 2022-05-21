FROM jenkins/jenkins:lts-jdk11 AS jenkins-base

LABEL maintainer="Ivan Medaev"

USER root

RUN mkdir -p /var/jenkins_config/ \
    && chown -R jenkins:jenkins /var/jenkins_home /var/jenkins_config \
    && chmod -R 700 /var/jenkins_home /var/jenkins_config \
    && apt-get update \
    && apt-get -y install \
        apt-utils \
        vim \
        curl \
        net-tools \
        iproute2 \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/ \
    && rm -rf /tmp/* /var/tmp/*

USER jenkins

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
ENV CASC_JENKINS_CONFIG=/var/jenkins_config/jenkins.yaml

COPY --chown=jenkins:jenkins plugins.txt /var/jenkins_config/

RUN /usr/local/bin/install-plugins.sh < /var/jenkins_config/plugins.txt
