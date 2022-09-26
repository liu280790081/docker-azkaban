# BUILD: docker build --rm -t azkaban-executor .

FROM alpine

MAINTAINER Orange <280790081@qq.com>

#Replace with domestic mirror source
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk add --update openjdk8-jre curl bash && rm -rf /var/cache/apk/*

# Azkaban executor port
EXPOSE 12321 8081
