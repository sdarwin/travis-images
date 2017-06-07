FROM centos:6
MAINTAINER Sam Darwin

# Install Ansible and other requirements.
#RUN yum makecache fast \
# && yum -y install deltarpm epel-release \
# && yum -y update \
# && yum -y install \
#      ansible \
#      sudo \
#      which \
#      initscripts \
# && yum clean all

RUN yum makecache fast 
RUN yum install -y deltarpm epel-release initscripts
RUN yum install -y gcc openssl-devel python-devel sudo which libffi-devel
RUN yum install -y python-pip
RUN pip install ansible

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible && echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

CMD ["/sbin/init"]
