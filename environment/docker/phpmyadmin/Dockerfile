FROM phpmyadmin/phpmyadmin

ARG VERSION
ARG DOMAIN
ARG EMAIL

LABEL version = ${VERSION}
LABEL domain  = ${DOMAIN}
LABEL email   = ${EMAIL}

# Suppress docker-compose message with missing 'ServerName' directive
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
