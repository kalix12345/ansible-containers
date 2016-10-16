FROM phusion/baseimage:0.9.16

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Tell debconf to run in non-interactive mode
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y wget git zip

# Enable SSH loging provided by Baseimage docker and regenerate keys
RUN rm -f /etc/service/sshd/down
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
RUN mkdir -p /root/.ssh

# Permanently enable the insecure-key
RUN /usr/sbin/enable_insecure_key

RUN echo 'root:gns3' | chpasswd
RUN sed -i "s/#PermitRootLogin without-password/PermitRootLogin yes/" /etc/ssh/sshd_config
RUN sed -i "s/#ListenAddress 0.0.0.0/ListenAddress 0.0.0.0/" /etc/ssh/sshd_config
RUN sed -i "s/#ListenAddress ::/ListenAddress ::/" /etc/ssh/sshd_config

RUN useradd -m -p gns3 ansible 

RUN sudo -u ansible -- ssh-keygen -f /home/ansible/.ssh/id_rsa -t rsa -N ''

# Add ansible user to sudoers
RUN echo 'ansible  ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers


# Clean up APT
RUN apt-get clean && rm -rf /var/lib/apt/lists/* 

# start command
# /etc/init.d/ssh restart
