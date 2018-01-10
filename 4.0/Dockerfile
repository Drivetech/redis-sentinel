FROM redis:4.0.6-alpine@sha256:a5fd9334b28d6afdc8b84aad8a01056d8d1d849cb5a744919caf40d5b57597b2

ENV SENTINEL_QUORUM=2 SENTINEL_DOWN_AFTER=1000 SENTINEL_FAILOVER=1000 REDIS_PASSWORD=redis1234

RUN mkdir -p /redis

WORKDIR /redis

COPY sentinel.conf .
COPY sentinel-entrypoint.sh /usr/local/bin/

RUN chown redis:redis /redis/* && \
    chmod +x /usr/local/bin/sentinel-entrypoint.sh

EXPOSE 26379

CMD ["sentinel-entrypoint.sh"]
