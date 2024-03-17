ARG ARCH=TBD
ARG BASE_IMAGE=ubuntu:22.04
FROM --platform=${ARCH} ${BASE_IMAGE}

RUN apt-get update && apt-get install -y apache2 apache2-utils && apt clean

# Consume the build argument in the build stage
ARG ARCH
RUN bash -c 'echo "<!DOCTYPE html><html><body><h1>Hello from ${ARCH} Container!</h1></body></html>" \
      > /var/www/html/index.html'

EXPOSE 80
CMD apache2ctl -D FOREGROUND
