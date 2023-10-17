FROM php:8.2-fpm-bullseye AS base

WORKDIR /workspace

# timezone environment
ENV TZ=UTC \
  # locale
  LANG=en_US.UTF-8 \
  LANGUAGE=en_US:en \
  LC_ALL=en_US.UTF-8 \
  # composer environment
  COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

ARG USER_UID=1000

RUN apt-get update \
  && apt-get -y install --no-install-recommends \
  wget \
  curl \
  tar

RUN \
  useradd --shell /bin/bash --user-group --create-home appuser && \
  usermod --non-unique --uid ${USER_UID} appuser && \
  groupmod --non-unique --gid ${USER_UID} appuser
  
RUN \
  install -o appuser -g appuser -d / && \
  install -o appuser -g appuser -d /

COPY ./app/php/php.development.ini /usr/local/etc/php/php.ini

RUN \
  wget -P /tmp https://wordpress.org/wordpress-6.3.2.tar.gz \
  tar xzvf /tmp/wordpress-6.3.2.tar.gz \
  # chmod +x /tmp/wordpress \
  # cp -RT /tmp/wordpress /workspace \
  # chown -R appuser:appuser /workspace