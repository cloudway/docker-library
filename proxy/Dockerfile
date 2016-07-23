FROM icloudway/hipache:0.4.0

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

# add proxy updater service
ENV CLOUDWAY_VERSION 0.2.0
ARG CLOUDWAY_TGZ_URL="https://github.com/cloudway/platform/releases/download/v$CLOUDWAY_VERSION/cwman-$CLOUDWAY_VERSION-linux-amd64.tar.gz"
RUN curl -sSL "$CLOUDWAY_TGZ_URL" | tar -xz -C /usr/bin --strip-components=1

COPY add-mapping /usr/bin/
COPY cloudway.conf /usr/local/cloudway/conf/cloudway.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ENTRYPOINT ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
