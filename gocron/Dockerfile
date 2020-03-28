FROM amd64/alpine:3.10

LABEL maintainer="ChaosTong <easyulife@gmail.com>"

ENV GOCRON_VERSION 1.5.3

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories 

RUN apk add --no-cache bash \
    bash-doc \
    bash-completion

RUN apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && rm -rf /var/cache/apk/* \
    && /bin/bash

RUN addgroup -S app && \
    adduser -S -g app app  

VOLUME /app/conf
# expose /app/conf
# https://hub.docker.com/r/ouqg/gocron
WORKDIR /app

RUN chown -R app:app ./

EXPOSE 5920

RUN cd /app \
    &&  wget --no-check-certificate -c https://github.com/ouqiang/gocron/releases/download/v${GOCRON_VERSION}/gocron-node-v${GOCRON_VERSION}-linux-amd64.tar.gz \
    &&  tar zxvf gocron-node-v${GOCRON_VERSION}-linux-amd64.tar.gz  \
    &&  cd gocron-node-linux-amd64/ \
    &&  cp gocron-node /app \
    &&  cd /app \
    &&  wget --no-check-certificate -c https://github.com/ouqiang/gocron/releases/download/v${GOCRON_VERSION}/gocron-v${GOCRON_VERSION}-linux-amd64.tar.gz \
    &&  tar zxvf gocron-v${GOCRON_VERSION}-linux-amd64.tar.gz  \
    &&  cd gocron-linux-amd64/ \
    &&  cp gocron /app \
    &&  cd /app \
    &&  rm gocron-node-v${GOCRON_VERSION}-linux-amd64.tar.gz \
    &&  rm -rf gocron-node-linux-amd64 \
    &&  rm gocron-v${GOCRON_VERSION}-linux-amd64.tar.gz \
    &&  rm -rf gocron-linux-amd64/ 

USER app

# ENTRYPOINT ./gocron web