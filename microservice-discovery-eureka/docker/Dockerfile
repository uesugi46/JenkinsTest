FROM java:8-jdk-alpine
VOLUME /tmp
COPY minimum.jar app.jar
#COPY libs /libs
ENV JAVA_OPTS=""
ENTRYPOINT exec java ${JAVA_OPTS} -Djava.security.egd=file:/dev/./urandom -jar /app.jar
