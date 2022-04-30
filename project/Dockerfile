# pull official base image
FROM python:3.10.1-slim-buster

# create working directory
RUN mkdir -p /usr/src/app

# set working directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install system dependencies
RUN apt-get update \
    && apt-get -y install netcat gcc \
    && apt-get clean

# install python dependencies
RUN pip install --upgrade pip
COPY ./pyproject.toml .
COPY ./poetry.lock .
RUN pip install poetry
RUN poetry config virtualenvs.create false \
    && poetry install --no-ansi --no-interaction

# add app
COPY . .