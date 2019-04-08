FROM python:3.6

ENV PYTHONUNBUFFERED=1
ENV DEBIAN_FRONTEND noninteractive

WORKDIR /usr/src

RUN apt-get update -y --fix-missing && \
      apt-get install -y --no-install-recommends \
      mecab \
      libmecab-dev \
      mecab-ipadic-utf8 \
      make \
      curl \
      xz-utils \
      file \
      patch \
      locales

RUN echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen ja_JP.UTF-8 && \
    dpkg-reconfigure locales && \
    /usr/sbin/update-locale LANG=ja_JP.UTF-8

ENV LC_ALL=ja_JP.UTF-8
ENV LANG=ja_JP.UTF8

COPY ./Pipfile  ./
COPY ./Pipfile.lock ./

ENV PIPENV_VENV_IN_PROJECT=1

RUN pip install --upgrade pip
RUN pip install pipenv
RUN pipenv install --system --dev

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--allow-root"]
