FROM redis:3.2.12-alpine@sha256:e9083e10f5f81d350a3f687d582aefd06e114890b03e7f08a447fa1a1f66d967

ENV SENTINEL_QUORUM=2 SENTINEL_DOWN_AFTER=1000 SENTINEL_FAILOVER=1000 REDIS_PASSWORD=redis1234

RUN mkdir -p /redis

WORKDIR /redis

COPY sentinel.conf .
COPY sentinel-entrypoint.sh /usr/local/bin/

RUN chown redis:redis /redis/* && \
    chmod +x /usr/local/bin/sentinel-entrypoint.sh

EXPOSE 26379

CMD ["sentinel-entrypoint.sh"]
