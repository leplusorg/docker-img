FROM alpine:3.24.2@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-euo", "pipefail", "-c"]

RUN apk upgrade --no-cache \
    && apk add --no-cache \
    coreutils=9.11-r0 \
    curl=8.22.0-r0 \
    exiftool=13.55-r0 \
    git=2.54.0-r0 \
    imagemagick=7.1.2.30-r0 \
    optipng=7.9.1-r1 \
    py3-pip=26.1.2-r0 \
    python3=3.14.7-r1 \
    && apk cache --no-cache clean \
    && rm -rf /var/cache/apk/*

RUN adduser \
  --home "${USER_HOME}" \
  --uid "${USER_ID}" \
  --gecos "${USER_GECOS}" \
  --disabled-password \
  "${USER_NAME}"

USER "${USER_NAME}"

ENV HOME="${USER_HOME}"

WORKDIR "${HOME}"
