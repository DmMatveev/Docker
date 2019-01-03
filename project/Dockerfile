FROM python:3.7.2-slim-stretch

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN echo "root:Docker!" | chpasswd

WORKDIR /root/Store

COPY requirements.txt /root/Store/requirements.txt

RUN pip install -r requirements.txt