FROM amd64/alpine:3.10

LABEL maintainer="ChaosTong <easyulife@gmail.com>"

ENV GOCRON_VERSION 1.5.3

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories 

RUN apk add --no-cache bash \
    bash-doc \
    bash-completion \
    zsh \
    git \
    nodejs npm \
    python3

RUN git clone https://gitee.com/mirrors/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

RUN apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && rm -rf /var/cache/apk/* \
    && /bin/bash

RUN sed -i -e "s/bin\/ash/bin\/zsh/" /etc/passwd

ENV SHELL /bin/zsh

VOLUME /data

WORKDIR /app

EXPOSE 5921

RUN cd /app \
    &&  wget --no-check-certificate -c https://github.com/ouqiang/gocron/releases/download/v${GOCRON_VERSION}/gocron-node-v${GOCRON_VERSION}-linux-amd64.tar.gz \
    &&  tar zxvf gocron-node-v${GOCRON_VERSION}-linux-amd64.tar.gz  \
    &&  cd gocron-node-linux-amd64/ \
    &&  cp gocron-node /app \
    &&  cd /app \
    &&  rm gocron-node-v${GOCRON_VERSION}-linux-amd64.tar.gz \
    &&  rm -rf gocron-node-linux-amd64

ENTRYPOINT "/app/gocron-node -allow-root"