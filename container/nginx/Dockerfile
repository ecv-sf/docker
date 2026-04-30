ARG NGINX_VERSION=1.29.8
FROM nginx:${NGINX_VERSION}-alpine

ARG SERVER_NAME
RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/
RUN rm /etc/nginx/conf.d/default.conf
COPY ecv.conf /etc/nginx/conf.d/
RUN sed -i "s/_SERVER_NAME_/${SERVER_NAME}/g" /etc/nginx/conf.d/ecv.conf


EXPOSE 80 8080

CMD ["nginx", "-g", "daemon off;"]