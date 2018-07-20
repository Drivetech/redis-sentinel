FROM redis:4.0.9-alpine@sha256:fc13b47aca9b5b53f625efe91bcd5cc44c637e80a81e5b223d5a98a6eac7ceb2

ENV SENTINEL_QUORUM=2 SENTINEL_DOWN_AFTER=1000 SENTINEL_FAILOVER=1000 REDIS_PASSWORD=redis1234

RUN mkdir -p /redis

WORKDIR /redis

COPY sentinel.conf .
COPY sentinel-entrypoint.sh /usr/local/bin/

RUN chown redis:redis /redis/* && \
    chmod +x /usr/local/bin/sentinel-entrypoint.sh

EXPOSE 26379

CMD ["sentinel-entrypoint.sh"]
