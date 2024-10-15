FROM nginx:latest

COPY default.conf /etc/nginx/conf.d/default.conf

COPY html /usr/share/nginx/html

COPY ssl/nginx-selfsigned.crt /etc/ssl/nginx-selfsigned.crt
COPY ssl/nginx-selfsigned.key /etc/ssl/nginx-selfsigned.key

EXPOSE 8080 445