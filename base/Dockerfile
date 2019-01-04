FROM debian:stretch-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG en_US.UTF-8

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends apt-utils; \
    apt-get install -y --no-install-recommends \
		ca-certificates \
		locales \
		tzdata; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen; \
    echo "ru_RU.UTF-8 UTF-8" >> /etc/locale.gen; \
    dpkg-reconfigure -f noninteractive locales; \
    update-locale LANG=en_US.UTF-8; \
    ln -fs /usr/share/zoneinfo/Europe/Moscow /etc/localtime; \
    dpkg-reconfigure -f noninteractive tzdata

