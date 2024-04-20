FROM ubuntu:latest

RUN apt -y update && apt clean all

ENV TZ=Asia/Tokyo
RUN apt -y install tzdata
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# install sudo
RUN apt -y install sudo ssh openssh-client software-properties-common less

# install docker client
RUN apt -y install \
    python3-pip \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    software-properties-common

# install docker ce cli
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

RUN apt update && apt install -y docker-ce-cli

# install ansible
RUN add-apt-repository --yes --update ppa:ansible/ansible && \
    apt update && \
    apt -y install ansible

# setttings
ADD ansible.cfg /etc/ansible
