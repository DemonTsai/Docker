#######################################################
# This dockerfile builds a opendaylight develop       #
# environment                                         #
#                                                     #
# Author: Demon Tsai                                  #
# Repository: demontsai/opendaylight                  #
# Version: develop                                    #
#                                                     #
#######################################################

FROM demontsai/maven:3.3.9

MAINTAINER Demon Tsai demontsai@estinet.com


##### Update system and install apps
RUN     apt-get -qq update && apt-get -qqy install openssh-server

##### Maven setting
RUN     mkdir /home/ubuntu/.m2
COPY    settings.xml /home/ubuntu/.m2/settings.xml

##### Expose port for controller
EXPOSE  6633 8181

##### SSH setting
RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t ecdsa -N "" -f /home/ubuntu/.ssh/id_ecdsa
RUN     sudo -u ubuntu /usr/bin/ssh-keygen -t rsa -N "" -f /home/ubuntu/.ssh/id_rsa
RUN     mkdir -p /var/run/sshd
RUN 	echo "/usr/sbin/sshd -D" >> $ENTRYPOINT
EXPOSE  22

##### Sync source code folder
VOLUME  ["/home/ubuntu/code"]

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

##### Command
ENTRYPOINT $ENTRYPOINT


##################################################
##### Environment
#ENV     MVN_SETTING_URL     https://raw.githubusercontent.com/opendaylight/odlparent/master/settings.xml
#RUN     wget -q -O - $MVN_SETTING_URL > ~/.m2/settings.xml
