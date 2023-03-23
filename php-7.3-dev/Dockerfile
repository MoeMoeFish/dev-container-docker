FROM mcr.microsoft.com/devcontainers/base:jammy

COPY sources.list /etc/apt

# dependencies required for running "phpize"
# (see persistent deps below)
ENV PHPIZE_DEPS \
		autoconf \
		dpkg-dev \
		file \
		g++ \
		gcc \
		libc-dev \
		make \
		pkg-config \
		re2c

# persistent / runtime deps
RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		$PHPIZE_DEPS \
		ca-certificates \
		curl \
		iputils-ping \
		iputils-tracepath \
		iputils-arping \
		iputils-clockdiff \
		xz-utils;

RUN set -eux; \
	curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -; \
	apt-get install -y nodejs;

RUN set -eux; \
	apt-get install -y software-properties-common ca-certificates lsb-release apt-transport-https;

RUN set -eux; \
	add-apt-repository ppa:ondrej/php; \
	apt-get update; \
	apt-get -y --no-install-recommends install \
		php7.3 \
		php7.3-curl \
		php7.3-xml \
		php7.3-uuid \
		php7.3-ssh2 \
		php7.3-redis \
		php7.3-mysql \
		php7.3-json \
		php7.3-http \
		php7.3-imagick \
		php7.3-ds \
		php7.3-dev \
		php7.3-decimal \
		php7.3-gd \
		php7.3-raphf \
		php7.3-zip \
		php7.3-propro \
		php7.3-fpm;

RUN set -exu; \
	mkdir -p /run/php/; \
	chmod 777 /run/php;

RUN set -exu; \
	apt-get install -y nginx;

RUN set -exu; \
	apt-get upgrade -y;
	
RUN sed -i 's/worker_processes auto;/worker_processes 2;/' /etc/nginx/nginx.conf



CMD php-fpm7.3;
