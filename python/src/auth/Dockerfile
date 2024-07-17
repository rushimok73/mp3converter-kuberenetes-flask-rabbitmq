FROM python:3.10-slim-bullseye

RUN apt-get update \
  && apt-get install -y --no-install-recommends --no-install-suggests \
  build-essential \
  wget \
  curl \
  gnupg \
  default-libmysqlclient-dev \
  && wget https://downloads.mariadb.com/MariaDB/mariadb_repo_setup \
  && chmod +x mariadb_repo_setup \
  && ./mariadb_repo_setup --mariadb-server-version=10.6 \
  && apt-get update \
  && apt-get install -y --no-install-recommends --no-install-suggests \
  pkg-config \
  libmariadb3 \
  libmariadb-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /app
COPY ./requirements.txt /app
RUN pip install --no-cache-dir --requirement /app/requirements.txt
COPY . /app

EXPOSE 5000

CMD ["python3", "server.py"]