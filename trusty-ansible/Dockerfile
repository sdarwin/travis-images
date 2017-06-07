FROM ubuntu:14.04
MAINTAINER Sam Darwin

# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       software-properties-common \
    && rm -Rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean
# Install Ansible.
#RUN apt-add-repository -y ppa:ansible/ansible \
#    && apt-get update \
#    && apt-get install -y --no-install-recommends \
#       ansible \
#    && rm -rf /var/lib/apt/lists/* \
#    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
#    && apt-get clean

RUN apt-get install -y software-properties-common \
  && apt-add-repository -y universe \
  && apt-get update -y \
  && apt-get install -y libssl-dev \
  && apt-get install -y python-dev \
  && apt-get install -y libffi-dev 
RUN apt-get install -y python-pip
RUN pip install ansible

# Install Ansible inventory file
RUN mkdir /etc/ansible && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

# Workaround for pleaserun tool that Logstash uses
RUN rm -rf /sbin/initctl && ln -s /sbin/initctl.distrib /sbin/initctl
