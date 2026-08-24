FROM python:3.10

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /

RUN useradd -u 1000 -m app

RUN apt-get update && \
    apt-get install -y \
    pcre2-utils \
    libpcre2-dev \
    build-essential \
    linux-libc-dev \
    libffi-dev \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www/app && mkdir /app

COPY Pipfile* /app

RUN cd /app && pip install pipenv && pipenv install --system --deploy

COPY . /app

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "-s", "/var/www/app/app.sock", "--manage-script-name", "--mount", "/=app:app"]