#######################################################
# This dockerfile builds a maven environment          #
#                                                     #
#                                                     #
# Author: Demon Tsai                                  #
# Repository: demontsai/maven:3.3.9                   #
# Version: 1.0                                        #
#                                                     #
#######################################################

FROM demontsai/java:jdk7

MAINTAINER Demon Tsai demontsai@estinet.com


##### Environment
ENV     MVN_VERSION         3.3.9
ENV     MVN_FOLDER_NAME     apache-maven-$MVN_VERSION
ENV     MVN_TAR_FILE_NAME   $MVN_FOLDER_NAME-bin.tar.gz
ENV     MAVEN_OPTS '-Xmx2048m -XX:MaxPermSize=1024m'

##### Maven install
COPY    $MVN_TAR_FILE_NAME $MVN_TAR_FILE_NAME
RUN     tar xzvf $MVN_TAR_FILE_NAME
RUN     ln -s ~/$MVN_FOLDER_NAME/bin/mvn /usr/bin/mvn

##### Clean
RUN     apt-get clean
RUN     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/*.tar.gz
