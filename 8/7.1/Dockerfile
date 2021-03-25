FROM michaeltigr/toolbox-php:7.1-0.2.1.8

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

ENV NVM_DIR /usr/local/nvm

# Profile
RUN echo 'export NVM_DIR="/usr/local/nvm"' >> /etc/profile.d/nvm.sh \
    && echo '[ -s "${NVM_DIR}/nvm.sh" ] && . "${NVM_DIR}/nvm.sh"  # This loads nvm' >> /etc/profile.d/nvm.sh \
    && echo '[ -s "${NVM_DIR}/bash_completion" ] && . "${NVM_DIR}/bash_completion" # This loads nvm bash_completion' >> /etc/profile.d/nvm.sh

RUN mkdir -p ${NVM_DIR} \
    && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

ENV NODE_VERSION v8.17.0
ENV PATH /usr/local/nvm/versions/node/${NODE_VERSION}/bin:${PATH}

RUN source ${NVM_DIR}/nvm.sh \
    && nvm install -s ${NODE_VERSION} \
    && nvm alias default ${NODE_VERSION} \
    && nvm use --delete-prefix default \
    && rm -rf ${NVM_DIR}/.cache

RUN source ${NVM_DIR}/nvm.sh \
    && npm install -g yarn gulp-cli grunt-cli bower \
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
