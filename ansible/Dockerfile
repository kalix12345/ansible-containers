FROM phusion/baseimage

CMD ["/sbin/my_init"]


RUN add-apt-repository ppa:fkrull/deadsnakes
# Install some tools to the minimal image
RUN apt-get update && apt-get install -y wget iputils-ping mtr nmap iperf socat vim nano jq curl links iputils-ping dnsutils rsync openssl
RUN apt-get update && apt-get install -y wget python3.6 python2.7 python-dev
RUN apt-get install -y python-pip python3-pip python-setuptools python3-setuptools
RUN apt-get install -y build-essential libssl-dev libffi-dev

# Install ansible
RUN pip install ansible

# Create user ansible & generate keypair
RUN useradd --create-home --home-dir /home/ansible ansible \		
    && chown -R ansible:ansible /home/ansible		
USER ansible
RUN ssh-keygen -f /home/ansible/.ssh/id_rsa -t rsa -N ''
RUN mkdir /home/ansible/playbook

USER root
RUN echo root:gns3d0cker | toto123

# Add ansible to sudoers
RUN echo 'ansible  ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Clean up APT		
RUN apt-get clean && rm -rf /var/lib/apt/lists/* 

COPY backup /usr/bin/backup
COPY restore /usr/bin/restore
RUN chmod a+x /usr/bin/backup
RUN chmod a+x /usr/bin/restore

RUN mkdir /etc/ansible

# Create & mount backup directory
RUN mkdir /backup
VOLUME /backup

