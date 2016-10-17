FROM ansible/ansible:ubuntu1604

# Add ansible user to sudoers
RUN echo 'ansible  ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

RUN apt-get update && apt-get install -y vim nano ssh
RUN pip install ansible

CMD ["/sbin/init"]
