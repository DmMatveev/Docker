FROM base AS builder

ENV PYTHON_VERSION 3.7.2
ENV PYTHON_PIP_VERSION 18.1

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		libncursesw5-dev \
		libreadline-dev \
		libsqlite3-dev \
		libexpat1-dev \
		libgdbm-dev \
		liblzma-dev \
		libffi-dev \
		libssl-dev \
		libbz2-dev \
		zlib1g-dev \
		libc6-dev \
		dpkg-dev \
		uuid-dev \
		apt-utils \
		xz-utils \
		atool \
		make \
		wget \
		gcc \
		gnupg \
		dirmngr

RUN set -ex; \
    wget -q -O Python.tgz "https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz"; \
    aunpack Python.tgz; \
    rm Python.tgz; \
    cd Python-$PYTHON_VERSION; \
	./configure \
        --enable-loadable-sqlite-extensions \
		--enable-shared; \
		#--enable-optimizations; \
	make -j "$(nproc)"; \
	make -j "$(nproc)" check; \
	make install; \
	rm -r /Python-$PYTHON_VERSION

RUN pip3 install --upgrade setuptools pip
