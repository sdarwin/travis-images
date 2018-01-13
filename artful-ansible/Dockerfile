FROM ubuntu:17.10
MAINTAINER Sam Darwin

# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       python-software-properties \
       software-properties-common \
       rsyslog systemd systemd-cron sudo \
    && rm -Rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean
RUN sed -i 's/^\($ModLoad imklog\)/#\1/' /etc/rsyslog.conf
#ADD etc/rsyslog.d/50-default.conf /etc/rsyslog.d/50-default.conf

# Install Ansible
#RUN add-apt-repository -y ppa:ansible/ansible \
#  && apt-get update \
#  && apt-get install -y --no-install-recommends \
#     ansible \
#  && rm -rf /var/lib/apt/lists/* \
#  && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
#  && apt-get clean
RUN apt-get install -y software-properties-common \
  && apt-add-repository -y universe \
  && apt-get update -y \
  && apt-get install -y libssl-dev
RUN apt-get install -y python-pip
RUN pip install ansible

COPY initctl_faker .
RUN chmod +x initctl_faker && rm -fr /sbin/initctl && ln -s /initctl_faker /sbin/initctl

# Install Ansible inventory file
RUN mkdir -p /etc/ansible && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts
