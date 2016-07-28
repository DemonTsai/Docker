FROM ubuntu:14.04

ENV DHCP_CFG /etc/dhcp/dhcpd.conf
ENV PATH $PATH:/opt/dhcp

RUN echo "Asia/Taipei" > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata \
    && sed -i 's/tw.archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list \
    && sed -i 's/us.archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list \
    && sed -i 's/archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y isc-dhcp-server supervisor arping \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && bash -c "cp /etc/dhcp/dhcpd.conf{,.orig}" && sed -i '/#.*/ d' $DHCP_CFG && sed -i '/^$/ d' $DHCP_CFG \
    && mkdir /opt/dhcp

WORKDIR /opt/dhcp

COPY supervisord.isc-dhcp-server.conf /etc/supervisor/conf.d/
COPY script/* /opt/dhcp/

CMD ["/usr/bin/supervisord", "-n"]

