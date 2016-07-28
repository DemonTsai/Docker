#######################################################
# This dockerfile builds a clean debian 7.7           #
#                                                     #
# Author: Demon Tsai                                  #
#                                                     #
# Version: 1.0                                        #
#                                                     #
#######################################################

FROM    debian:7.7

MAINTAINER Demon Tsai demontsai@estinet.com


##### Update system and install apps
RUN     apt-get update -qq
RUN     apt-get install -qqy sudo
#RUN    apt-get install -qqy libnet-ifconfig-wrapper-perl

##### Create an user account and assign password to it
#RUN     useradd -m ubuntu && adduser ubuntu sudo && chsh -s /bin/bash ubuntu
RUN     useradd -m -G sudo -s /bin/bash ubuntu
RUN     echo "ubuntu:ubuntu" | chpasswd

##### Join the user to sudoers
RUN     echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' > /tmp/ubuntu
RUN     echo 'Defaults:ubuntu !requiretty' >> /tmp/ubuntu
RUN     chmod 0440 /tmp/ubuntu
RUN     chown root:root /tmp/ubuntu
RUN     mv /tmp/ubuntu /etc/sudoers.d/ubuntu

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

################################
##### COPY config to container and run it
#COPY    config /home/ubuntu/config
#RUN     /home/ubuntu/config

##### SSH setting
#RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t ecdsa -N "" -f /home/ubuntu/.ssh/id_ecdsa
#RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t rsa -N "" -f /home/ubuntu/.ssh/id_rsa
#RUN     mkdir -p /var/run/sshd

##### Screen setting
#COPY    screenrc /etc/
#RUN     mkdir -p /var/run/screen
#RUN     chmod 0777 /var/run/screen

##### Vim
#COPY    vimrc.local /etc/vim/
