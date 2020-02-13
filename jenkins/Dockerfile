FROM jenkins/jenkins:lts

USER root
# install docker
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common 
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update  -qq \
    && apt-get install docker-ce -y
RUN usermod -aG docker jenkins
# install docker compose
RUN curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose
# install ansible
RUN add-apt-repository \
    "deb http://ppa.launchpad.net/ansible/ansible/ubuntu bionic main"
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
RUN apt-get update -qq \
    && apt-get install -y ansible=2.9.4-1ppa~bionic jq
# install kubectl
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - \
    && echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list \
    && apt update -qq \
    && apt install -y kubectl
# install helm
RUN wget --quiet https://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-linux-amd64.tar.gz \
    && tar -zxvf helm-v2.11.0-linux-amd64.tar.gz \
    && mv linux-amd64/helm /usr/local/bin/helm \
    && rm -r linux-amd64/ \
    && rm helm-v2.11.0-linux-amd64.tar.gz