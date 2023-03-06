FROM alpine:3.17
MAINTAINER Guillaume Chauveau <docker@appus.fr>

ENV MAILCATCHER_VERSION=0.8.2
ENV TIMEZONE="Europe/Paris"

RUN apk add --update ruby ruby-dev ruby-io-console ruby-json ruby-bigdecimal bash sqlite sqlite-dev openssl-dev build-base \
  && gem install json \
  && gem install mailcatcher -v $MAILCATCHER_VERSION \
  && apk del --update build-base openssl-dev ruby-dev \
  && apk add --update libstdc++ \
  && rm -rf /var/cache/apk/*

EXPOSE 1025 1080

CMD ["mailcatcher", "-f", "--ip=0.0.0.0"]