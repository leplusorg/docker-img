FROM alpine:3.16.0

# hadolint ignore=DL3018
RUN apk --update --no-cache add exiftool imagemagick \
    && rm -rf /var/cache/apk/*
