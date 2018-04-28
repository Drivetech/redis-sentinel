FROM redis:3.2.11-alpine@sha256:2ceb7ddf7cba73ebbaca849f9c4646869145d1f9aed1eb127856f66ecf5aad9a

ENV SENTINEL_QUORUM=2 SENTINEL_DOWN_AFTER=1000 SENTINEL_FAILOVER=1000 REDIS_PASSWORD=redis1234

RUN mkdir -p /redis

WORKDIR /redis

COPY sentinel.conf .
COPY sentinel-entrypoint.sh /usr/local/bin/

RUN chown redis:redis /redis/* && \
    chmod +x /usr/local/bin/sentinel-entrypoint.sh

EXPOSE 26379

CMD ["sentinel-entrypoint.sh"]
