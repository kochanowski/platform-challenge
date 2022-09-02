FROM python:3.9.7-slim

ENV PYTHONUNBUFFERED 1

RUN useradd -ms /bin/bash docker-user
WORKDIR /code

COPY ./code/requirements.txt .

RUN /usr/local/bin/python -m pip install --upgrade pip \
  && pip install --no-cache-dir -r requirements.txt

COPY ./code .

RUN chown -R docker-user:docker-user /code

#USER docker-user
