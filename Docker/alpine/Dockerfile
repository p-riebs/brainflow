FROM alpine:latest

# This hack is widely applied to avoid python printing issues in docker containers.
# See: https://github.com/Docker-Hub-frolvlad/docker-alpine-python3/pull/13
ENV PYTHONUNBUFFERED=1

RUN echo "**** install Python and git ****" && \
    apk add --no-cache python3 git && \
    if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi && \
    \
    echo "**** install pip and setup packages****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade pip setuptools wheel && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi

RUN apk add --no-cache python3 git cmake bash make gcc g++ python3-dev

RUN echo "**** install brainflow and its python package ****" && \
 git clone -n https://github.com/p-riebs/brainflow.git && \
 cd brainflow && \
 git checkout master && \
 bash ./tools/build_linux.sh && \
 cd python-package && \
 python3 -m pip install -U . && \
 rm -rf /var/cache/apk/* && \
 rm -rf /brainflow
