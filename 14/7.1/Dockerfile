FROM michaeltigr/toolbox-php:7.1-latest

LABEL maintainer "Michael Molchanov <mmolchanov@adyax.com>"

USER root

ENV HOME /root
ENV NVM_DIR $HOME/.nvm

# Profile
RUN echo 'export NVM_DIR="$HOME/.nvm"' >> "$HOME/.bashrc"
RUN echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> "$HOME/.bashrc"
RUN echo '[ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion" # This loads nvm bash_completion' >> "$HOME/.bashrc"

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

RUN mkdir -p $NVM_DIR

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash

RUN source $NVM_DIR/nvm.sh \
  && source $NVM_DIR/nvm.sh \
  && nvm install -s v14.5.0 \
  && nvm alias default v14.5.0 \
  && nvm use --delete-prefix default

ENV PATH $HOME/.yarn/bin:$HOME/.nvm/versions/node/v14.5.0/bin:$PATH

RUN source $NVM_DIR/nvm.sh \
  && npm install -g gulp-cli grunt-cli bower \
  && curl -o- -L https://yarnpkg.com/install.sh | bash \
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