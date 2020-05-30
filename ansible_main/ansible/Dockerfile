FROM centos:7 as ansible_runner
ENV PS1 '$(whoami):$(pwd)\\$ '
ARG USER=ansible
ARG PASS=ansible
ARG UID=1000
ARG GID=1000
RUN yum update -y
COPY requirements-yum.txt /tmp/requirements-yum.txt
RUN yum install -y $(strings -1 /tmp/requirements-yum.txt | tr '\n' ' ')
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --upgrade -r /tmp/requirements.txt
RUN useradd -m ${USER} --uid=${UID} && echo "${USER}:${PASS}" | \
      chpasswd
USER ${UID}:${GID}
WORKDIR /home/${USER}