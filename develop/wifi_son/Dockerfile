#######################################################
# This dockerfile builds a clean ubuntu 14.04 and     #
# including samba, ssh, etc..., basic apps.           #
#                                                     #
# Author: Demon Tsai                                  #
#                                                     #
# Version: 1.0                                        #
#                                                     #
#######################################################

FROM demontsai/ubuntu:14.04

MAINTAINER Demon Tsai demontsai@estinet.com


##### Update system and install apps
RUN     apt-get update -qq
RUN     apt-get install -qqy openssh-server git gcc make autoconf

##### SSH setting
RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t ecdsa -N "" -f /home/ubuntu/.ssh/id_ecdsa
RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t rsa -N "" -f /home/ubuntu/.ssh/id_rsa
RUN     mkdir -p /var/run/sshd
RUN     echo "/usr/sbin/sshd -D" >> $ENTRYPOINT
EXPOSE  22

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

##### Command
ENTRYPOINT $ENTRYPOINT
