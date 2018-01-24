FROM redis:4.0.6-alpine@sha256:d471c77d4b9f50783e308d9e18d7f5b0701c013bd0c7d64c3983c584b2980654

ENV SENTINEL_QUORUM=2 SENTINEL_DOWN_AFTER=1000 SENTINEL_FAILOVER=1000 REDIS_PASSWORD=redis1234

RUN mkdir -p /redis

WORKDIR /redis

COPY sentinel.conf .
COPY sentinel-entrypoint.sh /usr/local/bin/

RUN chown redis:redis /redis/* && \
    chmod +x /usr/local/bin/sentinel-entrypoint.sh

EXPOSE 26379

CMD ["sentinel-entrypoint.sh"]
