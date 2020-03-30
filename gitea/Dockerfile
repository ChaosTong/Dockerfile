FROM amd64/alpine:3.10
LABEL maintainer="easyulife@gmail.com"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    rm -rf /var/cache/apk/*

EXPOSE 22 3000

RUN apk --no-cache add \
    bash \
    ca-certificates \
    curl \
    gettext \
    git \
    linux-pam \
    openssh \
    s6 \
    sqlite \
    su-exec \
    tzdata

RUN addgroup \
    -S -g 1000 \
    git && \
  adduser \
    -S -H -D \
    -h /data/git \
    -s /bin/bash \
    -u 1000 \
    -G git \
    git && \
  echo "git:$(dd if=/dev/urandom bs=24 count=1 status=none | base64)" | chpasswd

ENV USER git
ENV GITEA_CUSTOM /data/gitea

VOLUME ["/data"]

WORKDIR /app

RUN cd /app && wget -O gitea http://192.168.50.168:5000/share.cgi\?ssid\=0vQl8xo\&fid\=0vQl8xo\&filename\=gitea-1.11.3-linux-amd64\&openfolder\=forcedownload\&ep\= && \
    chmod +x gitea

USER git

ENTRYPOINT ["/app/gitea", "web"]