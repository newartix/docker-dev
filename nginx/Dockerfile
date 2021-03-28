FROM nginx:latest
RUN echo 'deb http://deb.debian.org/debian buster-backports main' > /etc/apt/sources.list.d/backports.list
RUN apt-get update && apt-get install -y certbot

