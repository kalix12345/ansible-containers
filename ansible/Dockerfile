FROM ansible/ansible:ubuntu1604

RUN useradd -m -p gns3 ansible 

RUN sudo -u ansible -- ssh-keygen -f /home/ansible/.ssh/id_rsa -t rsa -N ''

# Add ansible user to sudoers
RUN echo 'ansible  ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

RUN apt-get update && apt-get install -y ssh
RUN pip install ansible

CMD ["/sbin/init"]
