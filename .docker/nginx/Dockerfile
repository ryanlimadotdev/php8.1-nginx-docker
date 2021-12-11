FROM nginx:1.21.4-alpine

#Installing bash (Optionally)
RUN apk update && apk add bash

#Changing the default configurations for NGINX
RUN rm /etc/nginx/conf.d/default.conf
COPY ./default.conf /etc/nginx/conf.d
