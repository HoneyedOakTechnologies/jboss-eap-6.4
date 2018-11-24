# jboss-eap-6.4 [![Build Status](https://travis-ci.org/daggerok/jboss-eap-6.4.svg?branch=master)](https://travis-ci.org/daggerok/jboss-eap-6.4)
Docker hub JBoss EAP 6.4 automation build based on centos7 / alpine3.8 images

[daggerok/jboss-eap-6.4](https://hub.docker.com/r/daggerok/jboss-eap-6.4/)

## tags

- [latest](https://github.com/daggerok/jboss-eap-6.4/blob/master/Dockerfile)

- [6.4.1-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.1-alpine/Dockerfile)
- [6.4.1-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.1-centos/Dockerfile)

- [6.4.0-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.0-alpine/Dockerfile)
- [6.4.0-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.0-centos/Dockerfile)

## usage

### health check

```Dockerfile

FROM daggerok/jboss-eap-6.4:6.4.1-alpine
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/health \
         || exit 1
ADD ./target/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war

```

### multi deployment

```Dockerfile

FROM daggerok/jboss-eap-6.4:6.4.0-centos
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

### remote debug

```Dockerfile

FROM daggerok/jboss-eap-6.4:latest
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
COPY ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

__ports__

- management: 9990, 9999
- web http: 8080
- https: 8443