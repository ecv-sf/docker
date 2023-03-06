ARG NODE_VERSION
FROM node:${NODE_VERSION}-alpine
MAINTAINER Guillaume Chauveau <docker@appus.fr>

RUN apk add --no-cache curl git
RUN curl -o- -L https://yarnpkg.com/install.sh | sh

CMD ["tail", "-F", "-n0" ,"/etc/hosts"]