#FROM python:3.8
#WORKDIR /app
#COPY requirements.txt .
#RUN python -m pip install -r requirements.txt
#COPY . .
#EXPOSE 5000
#CMD ["gunicorn", "workers=3", "--bind", "0.0.0.0:5000", "app:app"]

FROM python:3.7.10-slim-buster
LABEL maintainer="<redacted>"

RUN useradd -m <username> -s /bin/bash
WORKDIR /home/<username>

RUN apt-get update -yq && apt-get upgrade -yq && \
    apt-get install -yq build-essential make gcc g++ && \
    apt-get install -yq python3-dev build-essential && \
    apt-get install -yq curl libpq-dev libffi-dev apt-utils && \
    apt-get install -y git &&\
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV PIP_DISABLE_PIP_VERSION_CHECK=1

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt --compile --no-cache-dir

RUN cd /home/<username>

COPY --chown=<username>:<username> app app
COPY manage.py config.py ./

USER <username>