FROM python:3.4-slim

RUN apt-get update && apt-get install -y \
      gcc \
      gettext \
      mysql-client libmysqlclient-dev \
      postgresql-client libpq-dev \
      sqlite3 \
      nginx \
      supervisor \
    --no-install-recommends && rm -rf /var/lib/apt/lists/*

ENV DJANGO_VERSION 1.9.8
ENV PIP_INDEX_URL https://pypi.douban.com/simple

RUN pip install mysqlclient psycopg2 gunicorn virtualenv django=="$DJANGO_VERSION"
