FROM mongo:3.2.6

RUN apt-get update && apt-get install -y --no-install-recommends supervisor git curl ca-certificates && rm -rf /var/lib/apt/lists/*

ENV CLOUDWAY_ROOT /usr/local/cloudway
ENV CLOUDWAY_DOMAIN example.com

ENV CLOUDWAY_VERSION 0.2.0
ARG CLOUDWAY_TGZ_URL="https://github.com/cloudway/platform/releases/download/v$CLOUDWAY_VERSION/cloudway-broker-$CLOUDWAY_VERSION-linux-amd64.tar.gz"
RUN curl -sSL "$CLOUDWAY_TGZ_URL" | tar -xz --strip-components=1 -C /

RUN git clone git://github.com/cloudway/plugins.git \
 && ( cd plugins && ./install.sh ) \
 && rm -rf plugins

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY entrypoint.sh /usr/local/cloudway/entrypoint.sh
ENTRYPOINT ["/usr/local/cloudway/entrypoint.sh"]

WORKDIR $CLOUDWAY_ROOT
EXPOSE 6616
