FROM jenkins/jenkins:2.580.2-lts-jdk21

USER root
RUN apt-get update && apt-get install -y docker.io && rm -rf /var/lib/apt/lists/*
USER jenkins

RUN jenkins-plugin-cli --plugins \
    blueocean \
    docker-plugin \
    docker-workflow \
    git \
    prometheus \
    metrics