# jboss-eap-6.4
Patched JBoss EAP 6.4 (including __6.4.22 patch__) Docker automation build based on amazoncorretto:8 images

This image is located on [docker hun](https://hub.docker.com/r/daggerok/jboss-eap-6.4/) as `daggerok/jboss-eap-6.4`

## usage

[TODO]

### health check

```Dockerfile

FROM daggerok/jboss-eap-6.4:6.4.22-alpine
HEALTHCHECK --retries=33 \
            --timeout=1s \
            --interval=1s \
            --start-period=3s \
            CMD wget -q --spider http://127.0.0.1:8080/my-service/health || exit 1
COPY --chown=jboss ./target/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war

```

### multi deployment

```Dockerfile

FROM daggerok/jboss-eap-6.4:6.4.22-centos
COPY --chown=jboss ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

### remote debug

```Dockerfile

FROM daggerok/jboss-eap-6.4:latest
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"
EXPOSE 5005
# ...

```

_ports_

- management: 9990, 9999
- web http: 8080
- https: 8443

<!--

git reset --hard origin/master
git fetch -p -a --prune-tags --force --tags 

git tag -d $tagName
git push --delete origin $tagName

git tag 6.4.22-centos
git push origin --tags --force

git tag 6.4.22-alpine
git push origin --tags --force

-->
