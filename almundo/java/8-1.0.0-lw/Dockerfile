FROM openjdk:8-jre-alpine
MAINTAINER Franco Morinigo <franco.morinigo@almundo.com>

ARG APPLICATION_PORT=8080
ARG DEBUG_PORT=9010
ENV APPLICATION_PORT=$APPLICATION_PORT
ENV DEBUG_PORT=$DEBUG_PORT

# Install jq
RUN apk update \
 && apk add jq \
 && rm -rf /var/cache/apk/*

# Copy java startup script
COPY start.sh start.sh

CMD ["./start.sh"]

# Application port
EXPOSE $application_port

# JMX or Debugging port
EXPOSE $debug_port
