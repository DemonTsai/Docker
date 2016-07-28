FROM    demontsai/jenkins-slave:base


RUN     apt-get update && \
        apt-get install --no-install-recommends  --no-install-suggests -y python-pip && \
        apt-get clean && rm -rf /var/lib/apt/lists/* && \
        pip install robotframework robotframework-selenium2library
