ARG NODE_VERSION
FROM node:${NODE_VERSION}-alpine

LABEL maintainer="guillaume.chauveau@appus.fr"

# Installation Yarn
RUN apk add --no-cache curl git python2 make g++
RUN npm install
RUN curl -o- -L https://yarnpkg.com/install.sh | sh
RUN yarn add @symfony/webpack-encore --dev
RUN yarn add sass-loader node-sass --dev
RUN yarn add webpack-notifier --dev
RUN npm install -g bower
RUN echo '{ "allow_root": true }' > /root/.bowerrc

CMD ["tail", "-F", "-n0" ,"/etc/hosts"]