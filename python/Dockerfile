FROM dmmatveev/base AS builder

ENV PYTHON_VERSION 3.7.2

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		libncursesw5-dev \
		libreadline-dev \
		libsqlite3-dev \
		libgdbm-dev \
		liblzma-dev \
		libffi-dev \
		libssl-dev \
		libbz2-dev \
		zlib1g-dev \
		libc6-dev \
		uuid-dev \
		dirmngr \
		gnupg \
		atool \
		make \
		wget \
		gcc

RUN set -ex; \
    wget -q -O Python.tgz "https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz"; \
    aunpack Python.tgz; \
    rm Python.tgz; \
    cd Python-$PYTHON_VERSION; \
	./configure \
		--enable-optimizations; \
	make -j "$(nproc)"; \
	make install; \
	rm -r /Python-$PYTHON_VERSION

RUN pip3 install --upgrade setuptools pip

RUN find /usr/local -depth -type d -name test -o -name tests -exec rm -rf '{}' \;
RUN find /usr/local -depth -type d -name '*.pyc' -o -name '*.pyo' -exec rm -rf '{}' \;

FROM dmmatveev/base

COPY --from=builder /usr/local/include /usr/local/include
COPY --from=builder /usr/local/share /usr/local/share
COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=builder /usr/local/lib /usr/local/lib

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		libffi-dev; \
	rm -rf /var/lib/apt/lists/*

RUN set -ex; \
    cd /usr/local/bin; \
	ln -s idle3 idle; \
	ln -s pydoc3 pydoc; \
	ln -s python3 python; \
	ln -s python3-config python-config; \
	ln -s pip3 pip

#RUN python3 -m test test_socket test_asyncio

