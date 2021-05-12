# OllivandersDockerCharlos16v

Exercise to dockerize a Flask API.

The image is available in DockerHub!
https://hub.docker.com/r/charlos16v/flaskapp


## RUN IT:
```shell
docker run -it --publish 80:5000 charlos16v/flaskapp
```


## Dockerfile:
```dockerfile
# First of all we are going to use a python3 slim buster image to generate a lightweight image.
FROM python:3-slim-buster
MAINTAINER Carlos Uriel <cdominguez@cifpfbmoll.eu>

# We indicate the port on wich the container listens for connections.
EXPOSE 5000

# We deactivate the generation of .pyc files inside the container and turn off the container buffering to facilitate the logging
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Generate the directory where we are going to put the source code, and we set it as WORKDIR.
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# We copy the requirements.txt file to the WORKDIR, and install the dependencies.
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r requirements.txt

# We copy the source code to the WORKDIR.
COPY . /usr/src/app

# We are going to use a declared user to avoid the default root user.
ENV USER=appuser
RUN adduser \
    --disabled-password \
    --home "$(pwd)" \
    --no-create-home \
    "$USER"
USER appuser

# We set the execution command to run the API.
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]
```
