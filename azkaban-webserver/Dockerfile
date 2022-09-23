# BUILD: docker build --rm -t azkaban-webserver .

FROM alpine

MAINTAINER Orange <280790081@qq.com>

ENV AZK_VERSION 0.1.0-SNAPSHOT

#Replace with domestic mirror source
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk add --update openjdk8-jre curl bash mysql-client && rm -rf /var/cache/apk/*

#install web-server
COPY azkaban-web-server-$AZK_VERSION.tar.gz /azkaban-web-server-$AZK_VERSION.tar.gz
RUN tar xzvf azkaban-web-server-$AZK_VERSION.tar.gz && \
    rm -fr azkaban-web-server-$AZK_VERSION.tar.gz

RUN mkdir azkaban-web-server-$AZK_VERSION/logs/
# Work around to run container as a daemon
RUN sed -i "s/&//" azkaban-web-server-$AZK_VERSION/bin/start-web.sh

ADD keystore azkaban-web-server-$AZK_VERSION/keystore
ADD conf/azkaban.properties azkaban-web-server-$AZK_VERSION/conf/azkaban.properties
ADD conf/azkaban-users.xml azkaban-web-server-$AZK_VERSION/conf/azkaban-users.xml
ADD conf/global.properties azkaban-web-server-$AZK_VERSION/conf/global.properties
ADD conf/log4j.properties azkaban-web-server-$AZK_VERSION/conf/log4j.properties

# Azkaban web server port
EXPOSE 8443

# Define default workdir
WORKDIR /azkaban-web-server-$AZK_VERSION

#CMD ["bin/start-web.sh;/bin/bash"]
CMD bash -C 'bin/start-web.sh';'bash'
