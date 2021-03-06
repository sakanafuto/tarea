FROM python:3.7-alpine

COPY requirements.txt /usr/src/app/requirements.txt

WORKDIR /usr/src/app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apk update \
    && apk add --virtual build-deps gcc python3-dev musl-dev \
    && apk add postgresql-dev \
    && pip list --outdate\
    && pip install --upgrade wheel\
    && pip install --upgrade setuptools\
    && pip install psycopg2\
    && apk del build-deps

RUN pip install --upgrade pip \
    && pip install pipenv

RUN pip install -r requirements.txt

COPY ./Pipfile /usr/src/app/Pipfile

COPY ./entrypoint.sh /usr/src/app/entrypoint.sh

RUN pipenv install --skip-lock --system --dev

COPY . /usr/src/app/

ENTRYPOINT ["/usr/src/app/entrypoint.sh"]