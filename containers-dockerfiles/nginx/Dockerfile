FROM nginx:latest

RUN apt-get -y update && apt-get -y --no-install-recommends upgrade && \
rm /etc/nginx/conf.d/default.conf
ADD ./symfony.conf /etc/nginx/conf.d/default.conf