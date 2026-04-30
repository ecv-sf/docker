ARG NODE_VERSION=25.9.0
FROM node:${NODE_VERSION}-alpine

RUN apk add --no-cache curl git
RUN curl -o- -L https://yarnpkg.com/install.sh | sh

CMD ["tail", "-F", "-n0" ,"/etc/hosts"]