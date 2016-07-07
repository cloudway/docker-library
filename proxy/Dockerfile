FROM hipache:0.3.1

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# patch the hipache package
RUN sed -i 's/"http-proxy": "1.0.2"/"http-proxy": "1.11.1"/' /hipache/package.json && \
    npm install -g /hipache --production && \
    mkdir -p /var/log/nginx

# make changes to redis config
RUN sed -i 's/daemonize yes/daemonize no/' /etc/redis/redis.conf

# add proxy updater service
ENV CLOUDWAY_VERSION 0.2.0
ARG CLOUDWAY_TGZ_URL="https://github.com/cloudway/platform/releases/download/v$CLOUDWAY_VERSION/cloudway-broker-$CLOUDWAY_VERSION-linux-amd64.tar.gz"
RUN curl -sSL "$CLOUDWAY_TGZ_URL" | tar -xz -C / --strip-components=1 cloudway/usr/bin/cwman

COPY add-mapping /usr/bin/
COPY cloudway.conf /usr/local/cloudway/conf/cloudway.conf
COPY config.json /hipache/config/config.json
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ENTRYPOINT ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
