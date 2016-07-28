#######################################################
# This dockerfile builds a opendaylight develop       #
# environment                                         #
#                                                     #
# Author: Demon Tsai                                  #
# Repository: demontsai/opendaylight                  #
# Version: release                                    #
#                                                     #
#######################################################

FROM demontsai/maven:3.3.9

MAINTAINER Demon Tsai demontsai@estinet.com


##### Update system and install apps
RUN     apt-get -qq update && apt-get -qqy install wget

##### Environment
ENV 	CONTROLLER_VERSION  1.0.2
ENV     CONTROLLER_NAME     E-Central-Enterprise-Controller
ENV 	CONTROLLER_URL	    'http://jenkins.estinet.com/job/controller-stable/lastStableBuild/com.estinet.controller$'$CONTROLLER_NAME/artifact/com.estinet.controller/$CONTROLLER_NAME

##### Maven setting
RUN     mkdir ~/.m2
COPY    settings.xml ~/.m2/settings.xml

##### Controller
RUN	    echo '[ -d \"$CONTROLLER_NAME-$CONTROLLER_VERSION\" ] || {' >> $ENTRYPOINT
RUN     echo '    rm -rf $CONTROLLER_NAME-*' >> $ENTRYPOINT
RUN 	echo '    wget $CONTROLLER_URL/$CONTROLLER_VERSION/$CONTROLLER_NAME-$CONTROLLER_VERSION.tar.gz' >> $ENTRYPOINT
RUN 	echo '    tar xzvf $CONTROLLER_NAME-$CONTROLLER_VERSION.tar.gz' >> $ENTRYPOINT
RUN     echo '    rm $CONTROLLER_NAME-*.tar.gz' >> $ENTRYPOINT
RUN	    echo '}' >> $ENTRYPOINT
RUN 	echo './$CONTROLLER_NAME-$CONTROLLER_VERSION/bin/karaf clean' >> $ENTRYPOINT

##### Expose port for controller
EXPOSE  6633 8181

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

##### Command
ENTRYPOINT $ENTRYPOINT

