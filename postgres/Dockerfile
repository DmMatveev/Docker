FROM base

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
		ca-certificates \
		apt-utils \
		netbase \
		dirmngr \
		procps \
		gnupg; \
	rm -rf /var/lib/apt/lists/*

ARG PG_VERSION=11.1

ENV PATH $PATH:/usr/local/pgsql/bin
ENV PGDATA /var/lib/pgsql

RUN set -ex; \
    apt-get update; \
	apt-get install -y --no-install-recommends \
	    libreadline-dev \
		zlib1g-dev; \
	rm -rf /var/lib/apt/lists/*

RUN set -eux; \
	groupadd -r postgres --gid=999; \
	useradd -r -g postgres --uid=999 --home=/var/lib/pgsql --shell=/bin/bash postgres; \
	mkdir -p /usr/local/pgsql; \
	mkdir -p /var/lib/pgsql; \
	chown -R postgres:postgres /var/lib/pgsql; \
	chown -R postgres:postgres /usr/local/pgsql

WORKDIR /var/lib/pgsql

RUN set -ex; \
    wget -q https://ftp.postgresql.org/pub/source/v$PG_VERSION/postgresql-$PG_VERSION.tar.gz; \
    aunpack postgresql-$PG_VERSION.tar.gz; \
    rm postgresql-$PG_VERSION.tar.gz; \
    cd postgresql-$PG_VERSION; \
    ./configure; \
    make -j "$(nproc)"; \
    su -c "make check" postgres; \
    make install-strip; \
    cd ../; \
    rm -rf postgresql-$PG_VERSION

USER postgres:postgres

RUN set -ex; \
    initdb



