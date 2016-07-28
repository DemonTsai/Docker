FROM    ubuntu:14.04


ENV     HOME        /root
ENV     LAUNCH      jenkins-slave.sh
ENV     SLAVE_NAME  slave
ENV     SECRET_KEY  ca8b4917f3032bc3ffdd8da6f191e17d4a5b3fae39ea71e9a3d06c3e80c4f53a


RUN     echo "Asia/Taipei" > /etc/timezone && \
        dpkg-reconfigure --frontend noninteractive tzdata && \
        apt-get update && \
        apt-get install --no-install-recommends  --no-install-suggests -y openjdk-7-jdk && \
        apt-get clean && rm -rf /var/lib/apt/lists/* && \
        echo '#!/bin/bash' > $HOME/$LAUNCH && \
        echo 'java -jar slave.jar -jnlpUrl http://master:8080/computer/$SLAVE_NAME/slave-agent.jnlp -secret $SECRET_KEY' >> $HOME/$LAUNCH && \
        chmod 755 $HOME/$LAUNCH

WORKDIR /root

COPY    slave.jar slave.jar

CMD     ["/root/jenkins-slave.sh"]
