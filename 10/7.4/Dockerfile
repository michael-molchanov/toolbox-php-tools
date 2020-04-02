FROM michaeltigr/toolbox-php:7.4-0.2.1.4

LABEL maintainer "Michael Molchanov <mmolchanov@adyax.com>"

USER root

# Install dependencies.
RUN apk add --update --no-cache \
  bash \
  binutils \
  ca-certificates \
  coreutils \
  curl \
  findutils \
  gcc \
  g++ \
  gifsicle \
  grep \
  libgcc \
  libjpeg-turbo-utils \
  libuv \
  libuv-dev \
  linux-headers \
  make \
  nasm \
  ncurses \
  openssl \
  optipng \
  python2 \
  util-linux \
  zlib-dev \
  && rm -rf /var/cache/apk/*

# Install nodejs and grunt.
RUN apk add --update --no-cache libuv nodejs npm nodejs-dev yarn \
  && rm -rf /var/cache/apk/* \
  && npm install -g gulp-cli grunt-cli bower \
  && node --version \
  && npm --version \
  && grunt --version \
  && gulp --version \
  && bower --version \
  && yarn versions

# Install compass.
RUN apk add --update --no-cache ruby ruby-dev \
  && rm -rf /var/cache/apk/* \
  && gem install --no-document compass