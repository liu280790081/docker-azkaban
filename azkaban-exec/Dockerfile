# BUILD: docker build --rm -t azkaban-executor .

FROM alpine

MAINTAINER Orange <280790081@qq.com>

USER root

ENV AZK_VERSION 0.1.0-SNAPSHOT

#Replace with domestic mirror source
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk add --update openjdk8-jre curl bash && rm -rf /var/cache/apk/*

COPY azkaban-exec-server-$AZK_VERSION.tar.gz /azkaban-exec-server-$AZK_VERSION.tar.gz
RUN tar xzvf azkaban-exec-server-$AZK_VERSION.tar.gz && \
    rm azkaban-exec-server-$AZK_VERSION.tar.gz
# Work around to run container as a daemon
RUN sed -i "s/&//" azkaban-exec-server-$AZK_VERSION/bin/start-exec.sh

ADD conf/azkaban.properties azkaban-exec-server-$AZK_VERSION/conf/azkaban.properties
ADD conf/global.properties azkaban-exec-server-$AZK_VERSION/conf/global.properties
ADD conf/log4j.properties azkaban-exec-server-$AZK_VERSION/conf/log4j.properties

# Azkaban executor port
EXPOSE 12321

# Define default workdir
WORKDIR /azkaban-exec-server-$AZK_VERSION

#CMD ["bin/start-exec.sh;/bin/bash"]
CMD bash -C 'bin/start-exec.sh';'bash'
