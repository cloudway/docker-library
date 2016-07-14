FROM debian:jessie

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

ENV CLOUDWAY_VERSION 0.2.0
ARG CLOUDWAY_TGZ_URL="https://github.com/cloudway/platform/releases/download/v$CLOUDWAY_VERSION/cloudway-broker-$CLOUDWAY_VERSION-linux-amd64.tar.gz"
RUN curl -sSL "$CLOUDWAY_TGZ_URL" | tar -xz -C / --strip-components=1 cloudway/usr/bin/cwman

COPY entrypoint.sh /usr/local/cloudway/entrypoint.sh
ENTRYPOINT ["/usr/local/cloudway/entrypoint.sh"]
EXPOSE 2200
