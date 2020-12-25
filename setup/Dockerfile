FROM jenkins/inbound-agent

USER root

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y wget
RUN wget -q https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_19.03.11~3-0~ubuntu-bionic_amd64.deb
RUN dpkg -i docker-ce-cli_19.03.11~3-0~ubuntu-bionic_amd64.deb
RUN groupadd docker
RUN usermod -aG docker jenkins
RUN newgrp docker

USER jenkins
ENTRYPOINT ["jenkins-agent"]
