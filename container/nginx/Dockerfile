ARG NGINX_VERSION
FROM nginx:${NGINX_VERSION}-alpine

LABEL maintainer="guillaume.chauveau@appus.fr"

# Copie des configurations
#RUN mkdir -p /etc/ssl
RUN rm /etc/nginx/nginx.conf
ADD nginx.conf /etc/nginx/
RUN rm /etc/nginx/conf.d/default.conf
ADD ecv.conf /etc/nginx/conf.d/

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 80
EXPOSE 443
EXPOSE 8081