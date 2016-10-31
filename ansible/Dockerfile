FROM ansible/ansible:ubuntu1604


# Install some tools to the minimal image
RUN apt-get update && apt-get install -y iputils-ping mtr nmap iperf socat vim nano curl links iputils-ping dnsutils rsync

# Install ansible
RUN pip install ansible

# Create user ansible & generate keypair
RUN useradd --create-home --home-dir /home/ansible ansible \		
    && chown -R ansible:ansible /home/ansible		
RUN sudo -u ansible -- ssh-keygen -f /home/ansible/.ssh/id_rsa -t rsa -N ''

# Add ansible to sudoers
RUN echo 'ansible  ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Clean up APT		
RUN apt-get clean && rm -rf /var/lib/apt/lists/* 

COPY backup /usr/bin/backup
COPY restore /usr/bin/restore
RUN chmod a+x /usr/bin/backup
RUN chmod a+x /usr/bin/restore

# Create playbook directory
RUN mkdir /home/ansible/playbook

# Create & mount backup directory
RUN mkdir /backup
VOLUME /backup

CMD ["/sbin/init"]
