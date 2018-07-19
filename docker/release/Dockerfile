FROM ezhang/todobackend-base:latest
MAINTAINER ezhang <ellison.zhang@activenetwork.com>

COPY target /wheelhouse

RUN . /appenv/bin/activate && \
    pip install --no-index -f /wheelhouse todobackend && \
    rm -rf /wheelhouse
