ARG NGINX_VERSION
FROM nginx:${NGINX_VERSION}-alpine
MAINTAINER Guillaume Chauveau <docker@appus.fr>

ARG SERVER_NAME
RUN rm /etc/nginx/nginx.conf
ADD nginx.conf /etc/nginx/
RUN rm /etc/nginx/conf.d/default.conf
ADD ecv.conf /etc/nginx/conf.d/
RUN sed "s/_SERVER_NAME_/$SERVER_NAME/g"


EXPOSE 80 8080

CMD ["nginx", "-g", "daemon off;"]