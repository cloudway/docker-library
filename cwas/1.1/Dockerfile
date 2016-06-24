FROM maven:3.3.9-jdk-8

ENV CWAS_HOME /usr/local/cwas
RUN mkdir -p "$CWAS_HOME"
WORKDIR $CWAS_HOME"

ENV CWAS_VERSION 1.1
ARG CWAS_TGZ_URL="http://dist-cloudway.rhcloud.com/pub/cloudway/server/$CWAS_VERSION/cloudway-server-$CWAS_VERSION-bin.tar.gz"
RUN curl -fSL "$CWAS_TGZ_URL" | tar -xzC $CWAS_HOME --strip-components=1
RUN apt-get update && apt-get install -y --no-install-recommends lsof apache2-utils bc && rm -rf /var/lib/apt/lists/*

EXPOSE 8080
CMD ["/usr/local/cwas/bin/run.sh"]
