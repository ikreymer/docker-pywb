FROM python:2.7
MAINTAINER Ilya Kreymer <ikreymer at gmail.com>

ENV VERSION 0.10.9

RUN pip install -e git+https://github.com/ikreymer/pywb.git@develop#egg=pywb-{VERSION}-dev certauth youtube-dl boto uwsgi gevent

RUN mkdir /uwsgi

COPY uwsgi.ini /uwsgi/

RUN mkdir /webarchive

COPY config.yaml /webarchive/

VOLUME /webarchive

WORKDIR /webarchive

EXPOSE 8080

CMD ["uwsgi", "/uwsgi/uwsgi.ini"]
