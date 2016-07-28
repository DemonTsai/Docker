#######################################################
# This dockerfile builds chilli                       #
#                                                     #
# Author: Demon Tsai                                  #
# Repository: demontsai/coovachilli:1.3.0             #
# Version: 1.0                                        #
#                                                     #
#######################################################

FROM demontsai/ubuntu:14.04

MAINTAINER Demon Tsai demontsai@estinet.com


##### Adjust time zone
RUN     echo "Asia/Taipei" > /etc/timezone
RUN     dpkg-reconfigure --frontend noninteractive tzdata

##### Update system and install apps
RUN     apt-get update
RUN     apt-get install -qqy iptables libssl-dev devscripts haserl debhelper

##### Environment
ENV     CHILLI_VERSION  1.3.0
ENV     CHILLI          coova-chilli-$CHILLI_VERSION

##### Install chilli
COPY    $CHILLI.tar.gz  $CHILLI.tar.gz
COPY    chilli_*        /usr/sbin/
RUN     tar xzvf $CHILLI.tar.gz
WORKDIR $CHILLI
RUN     debuild -b -us -uc
RUN     dpkg -i ../*.deb
WORKDIR $HOME

#EXPOSE  18120/udp 1812/udp 1813/udp

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* *chilli*

#ENTRYPOINT  bash chilli_init


