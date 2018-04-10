FROM ubuntu:12.04

LABEL maintainer="xutongle@gmail.com"

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list \
    && apt-get update && apt-get install -y ca-certificates curl arj openjdk-6-jdk libapr1 libapr1-dev --no-install-recommends \
    && rm -r /var/lib/apt/lists/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime \
    && locale-gen zh_CN.UTF-8

WORKDIR /usr/local/tomcat

ENV LANG zh_CN.UTF-8
ENV LANGUAGE zh_CN:zh
ENV LC_ALL zh_CN.UTF-8

ENV TOMCAT_VERSION 6.0.53
ENV TOMCAT_TGZ_URL https://archive.apache.org/dist/tomcat/tomcat-6/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz

RUN curl -fSL ${TOMCAT_TGZ_URL} -o apache-tomcat-${TOMCAT_VERSION}.tar.gz \
    && tar -xvf apache-tomcat-${TOMCAT_VERSION}.tar.gz --strip-components=1 \
    && rm bin/*.bat \
    && rm -rf webapps/* \
    && rm apache-tomcat-${TOMCAT_VERSION}.tar.gz

sed -i 's/Connector port="8080"/Connector port="80"/g' /usr/local/tomcat/conf/server.xml

EXPOSE 80

CMD ["bin/catalina.sh","run"]