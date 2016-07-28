#######################################################
# This dockerfile builds freeradius                   #
#                                                     #
# Author: Demon Tsai                                  #
# Repository: demontsai/freeradius:3.0.11             #
# Version: 1.0                                        #
#                                                     #
#######################################################

FROM demontsai/ubuntu:14.04

MAINTAINER Demon Tsai demontsai@estinet.com


##### Update system and install apps
RUN     apt-get -qq update
RUN     apt-get -qqy install dpkg-dev ssl-cert quilt fakeroot\
        libcurl4-openssl-dev libcap-dev libjson0-dev libjson-c-dev \
        libreadline-dev libsqlite3-dev libtalloc-dev libwbclient-dev \
        libyubikey-dev libykclient-dev libmemcached-dev libhiredis-dev samba-dev
RUN     apt-get -y build-dep freeradius

##### Environment
ENV     FREERADIUS_VERSION  3.0.11
ENV     FREERADIUS          freeradius-server-$FREERADIUS_VERSION
ENV	    SQL_CFG             /etc/freeradius/mods-enabled/sql

##### Install freeradius
COPY    $FREERADIUS.tar.gz $FREERADIUS.tar.gz
COPY 	rad* /usr/sbin/
RUN     tar xzvf $FREERADIUS.tar.gz
WORKDIR $FREERADIUS
RUN     dpkg-buildpackage -b -uc
RUN     dpkg -i ../*.deb
WORKDIR $HOME
RUN	sed -i 's/FREERADIUS_OPTIONS=.*/FREERADIUS_OPTIONS=\"-f -X -P\"/1' /etc/default/freeradius
RUN 	cp /etc/freeradius/mods-available/sql $SQL_CFG
RUN 	sed -i 's/"rlm_sql_null"/"rlm_sql_mysql"/1' $SQL_CFG
RUN 	sed -i 's/dialect = "sqlite"/dialect = "mysql"/1' $SQL_CFG
RUN	    sed -i 's/.*read_clients = yes/    read_clients = yes/1' $SQL_CFG
RUN	    sed -i 's/.*server = "localhost"/    server = "localhost"/1' $SQL_CFG
RUN	    sed -i 's/.*port = 3306/    port = 3306/1' $SQL_CFG
RUN	    sed -i 's/.*login = "radius"/    login = "radius"/1' $SQL_CFG
RUN	    sed -i 's/.*password = "radpass"/    password = "radpass"/1' $SQL_CFG
RUN 	echo "radinit && service freeradius start" >> $ENTRYPOINT

EXPOSE  1812/udp 1813/udp

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* *freeradius*

##### Command
ENTRYPOINT $ENTRYPOINT

