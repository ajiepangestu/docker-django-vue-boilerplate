FROM debian:stretch-slim

RUN adduser --disabled-password --uid 10777 --gecos "" app

# Install Python and relevant dev tools
RUN apt-get update && apt-get install -y \
    build-essential \
    libffi-dev \
    libmariadbclient-dev \
    libssl-dev \
    python3 \
    python3-dev \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# default `python` and `pip` binaries to python3 and pip
RUN ln -s /usr/bin/python3 /usr/local/sbin/python \
    && ln -s /usr/bin/pip3 /usr/local/sbin/pip

# Install Python dependencies
WORKDIR /tmp
ADD requirements.txt requirements.txt
RUN pip install -r requirements.txt \
    && rm -rf requirements.txt

# Add project repository and own the directory contents
ADD . /home/app/app-core
RUN chown -R app /home/app/app-core

USER app
WORKDIR /home/app/app-core

EXPOSE 8000