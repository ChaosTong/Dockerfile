FROM alpine:latest

# Copy source code
COPY . /data

# Change working directory
WORKDIR /data

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk --update add --no-cache zsh && \
    apk add --no-cache git && \
    apk add --no-cache python3 && \
    rm -f /tmp/* /etc/apk/cache/*
    
# https://github.com/robbyrussell/oh-my-zsh.git
RUN git clone https://gitee.com/mirrors/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

RUN sed -i -e "s/bin\/ash/bin\/zsh/" /etc/passwd

ENV SHELL /bin/zsh