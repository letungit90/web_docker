FROM nginx:1.13.12

#COPY nginx.conf /etc/nginx/

RUN mkdir -p /var/www/default && touch /var/www/default/index.html

#COPY default.conf /etc/nginx/conf.d/

COPY vhost.conf /etc/nginx/conf.d/
