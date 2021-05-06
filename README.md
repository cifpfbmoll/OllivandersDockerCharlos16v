# OllivandersDockerCharlos16v

Exercise to dockerize a Flask API.

## Dockerfile:
```dockerfile
FROM python:3-alpine
MAINTAINER Carlos Uriel <cdominguez@cifpfbmoll.eu>

EXPOSE 5000

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r requirements.txt

COPY . /usr/src/app

ENV USER=docker
RUN adduser \
    --disabled-password \
    --home "$(pwd)" \
    --no-create-home \
    "$USER"
USER docker
CMD [ "python3", "./app.py" ]
```
