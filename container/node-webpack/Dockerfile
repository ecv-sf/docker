ARG NODE_VERSION
FROM node:${NODE_VERSION}-alpine

LABEL maintainer="guillaume.chauveau@appus.fr"

# Installation Yarn
RUN apk add --no-cache curl git
RUN curl -o- -L https://yarnpkg.com/install.sh | sh

CMD ["tail", "-F", "-n0" ,"/etc/hosts"]