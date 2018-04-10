FROM xutl/ubuntu:trusty

LABEL maintainer="xutongle@gmail.com"

RUN apt-get update && apt-get install -y curl openjdk-7-jdk libapr1 libapr1-dev --no-install-recommends \
    && rm -r /var/lib/apt/lists/*

ENV TOMCAT_VERSION 7.0.85
ENV TOMCAT_TGZ_URL https://archive.apache.org/dist/tomcat/tomcat-7/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz

WORKDIR /usr/local/tomcat

RUN curl -fSL ${TOMCAT_TGZ_URL} -o apache-tomcat-${TOMCAT_VERSION}.tar.gz \
    && tar -xvf apache-tomcat-${TOMCAT_VERSION}.tar.gz --strip-components=1 \
    && rm -f bin/*.bat \
    && rm -rf webapps/* \
    && rm -f apache-tomcat-${TOMCAT_VERSION}.tar.gz \
    && sed -i 's/Connector port="8080"/Connector port="80"/g' /usr/local/tomcat/conf/server.xml

EXPOSE 80

CMD ["bin/catalina.sh","run"]