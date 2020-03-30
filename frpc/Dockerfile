FROM alpine:latest

LABEL maintainer="ChaosTong <easyulife@gmail.com>"

ENV FRP_VERSION 0.32.0

# COPY qemu-i386-static /usr/bin

# Copy source code
COPY . /data

# Change working directory
WORKDIR /data

VOLUME ["/data"]

EXPOSE 7301
EXPOSE 7302
EXPOSE 7303

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk --update add --no-cache zsh && \
    apk add --no-cache git && \
    rm -f /tmp/* /etc/apk/cache/*
    
# https://github.com/robbyrussell/oh-my-zsh.git
RUN git clone https://gitee.com/mirrors/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

RUN sed -i -e "s/bin\/ash/bin\/zsh/" /etc/passwd

ENV SHELL /bin/zsh

RUN cd /root \
    &&  wget --no-check-certificate -c https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_386.tar.gz \
    &&  tar zxvf frp_${FRP_VERSION}_linux_386.tar.gz  \
    &&  cd frp_${FRP_VERSION}_linux_386/ \
    &&  cp frpc /usr/bin/ \
    &&  mkdir -p /etc/frp \
    &&  cd /root \
    &&  rm frp_${FRP_VERSION}_linux_386.tar.gz \
    &&  rm -rf frp_${FRP_VERSION}_linux_386/ 

# ENTRYPOINT /usr/bin/frpc -c /data/frpc_1.ini && /usr/bin/frpc -c /data/frpc_2.ini && /usr/bin/frpc -c /data/frpc_3.ini