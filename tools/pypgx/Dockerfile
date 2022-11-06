# Use latest Python base image
FROM python:3.8.15-slim-buster

# Install dependencies
RUN apt-get update && \
    apt-get install --yes git && \
    apt-get install --yes build-essential && \
    pip install --upgrade pip && \
    cd /opt  && \
    git clone --recursive https://github.com/sbslee/pypgx && \
    cd pypgx && \
    pip install .

WORKDIR /usr/app/src
ENV PATH="/opt/pypgx:${PATH}"

# by default /bin/sh is executed
CMD ["/bin/bash"]
