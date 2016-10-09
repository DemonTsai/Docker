FROM alpine


ENV VERSION=0.31

RUN apk --no-cache add nfs-utils

ADD https://github.com/ContainX/docker-volume-netshare/releases/download/v${VERSION}/docker-volume-netshare_${VERSION}_linux_amd64-bin /usr/bin/docker-volume-netshare
RUN chmod +x /usr/bin/docker-volume-netshare

ENTRYPOINT ["docker-volume-netshare"]
CMD ["nfs", "-o", "rsize=8192,wsize=8192"]
