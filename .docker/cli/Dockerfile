FROM php:7.3-fpm

RUN apt-get update && apt-get install -y \
git \
nano

RUN curl -v https://getcomposer.org/installer | php && \
   mv composer.phar /usr/local/bin/composer

ARG DOCKER_USER=dockeruser
ARG PUID=1000
ARG PGID=1000

RUN groupadd -g $PGID $DOCKER_USER && useradd -u $PUID -g $DOCKER_USER -m $DOCKER_USER && adduser $DOCKER_USER sudo

RUN chown $DOCKER_USER:$DOCKER_USER /usr/local/bin/composer

USER $DOCKER_USER

RUN mkdir -p /home/dockeruser/.composer/cache \
&& chown dockeruser:dockeruser /home/dockeruser/.composer/cache \
&& chmod -R 777 /home/dockeruser/.composer/cache

WORKDIR /var/www/html

EXPOSE 8080

RUN echo "export PATH=${PATH}:~/.composer/vendor/bin" >> ~/.bashrc

RUN . ~/.bashrc

# CMD [ "bash" ]