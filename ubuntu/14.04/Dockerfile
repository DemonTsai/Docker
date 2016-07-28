#######################################################
# This dockerfile builds a clean ubuntu 14.04         #
#                                                     #
# Author: Demon Tsai                                  #
# Repository: demontsai/ubuntu64:14.04                #
# Version: 1.0                                        #
#                                                     #
#######################################################

FROM ubuntu:14.04

MAINTAINER Demon Tsai demontsai@estinet.com


##### Environment
ENV 	ENTRYPOINT	/root/entrypoint.sh

##### Adjust time zone
RUN     echo "Asia/Taipei" > /etc/timezone
RUN     dpkg-reconfigure --frontend noninteractive tzdata

##### Create an user account and assign password to it
RUN     useradd -m  ubuntu && adduser ubuntu sudo && chsh -s /bin/bash ubuntu
RUN     echo "ubuntu:ubuntu" | chpasswd

##### Join the user to sudoers
RUN     echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' > /tmp/ubuntu
RUN     echo 'Defaults:ubuntu !requiretty' >> /tmp/ubuntu
RUN     chmod 0440 /tmp/ubuntu
RUN     chown root:root /tmp/ubuntu
RUN     mv /tmp/ubuntu /etc/sudoers.d/ubuntu

WORKDIR /root
RUN 	echo "root:root" | chpasswd

COPY    bashrc /home/ubuntu/.bashrc
RUN     chmod 0644 /home/ubuntu/.bashrc
RUN     chown ubuntu:ubuntu /home/ubuntu/.bashrc

COPY    bashrc /root/.bashrc
RUN     chmod 0644 /root/.bashrc
RUN     chown root:root /root/.bashrc

RUN     touch $ENTRYPOINT
RUN 	chmod 755 $ENTRYPOINT
RUN     echo "#!/bin/bash" >> $ENTRYPOINT

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


######################################
##### User
#USER    ubuntu
#ENV     HOME            /home/ubuntu
#ENV     CODE_PATH       $HOME/code
#ENV     INSTALL_PATH    $HOME/installation
#WORKDIR $HOME

##### Vim
#COPY    vimrc.local /etc/vim/

##### SSH setting
#RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t ecdsa -N "" -f /home/ubuntu/.ssh/id_ecdsa
#RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t rsa -N "" -f /home/ubuntu/.ssh/id_rsa
#RUN     mkdir -p /var/run/sshd
#EXPOSE  22

##### Screen setting
#COPY    screenrc /etc/
#RUN     mkdir -p /var/run/screen
#RUN     chmod 0777 /var/run/screen
