FROM ruby:2.7.7-bullseye
MAINTAINER Guillaume Chauveau <docker@appus.fr>

ENV MAILCATCHER_VERSION=0.8.2
ENV TIMEZONE="Europe/Paris"

RUN gem install mailcatcher
EXPOSE 1025 1080

CMD ["mailcatcher", "-f", "--ip=0.0.0.0"]