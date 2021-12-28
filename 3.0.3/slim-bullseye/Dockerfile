FROM ruby:3.0.3-slim-bullseye
LABEL maintainer="fillin Inc."

ENV LANG C.UTF-8
ENV APP_DIR /opt/rails
ARG NODE_MAJOR_VERSION=16
ENV RAILS_PORT 3000
ENV RAILS_IP 0.0.0.0

RUN apt -qq update \
      && apt install -y curl \
                    build-essential \
                    libbison-dev \
                    default-libmysqlclient-dev \
                    libpq-dev \
                    libxml2-dev \
                    libxslt1-dev \
                    jq \
                    ruby-dev \
                    imagemagick \
                    libvips \
                    ca-certificates

# Install Node & Yarn
RUN apt install -y curl \
      && apt remove -y cmdtest \
      && curl -sL https://deb.nodesource.com/setup_$NODE_MAJOR_VERSION.x | bash - \
      && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
      && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
      && apt -qq update \
      && apt install -y nodejs yarn


COPY startup.sh /root/startup.sh

RUN chmod +x /root/startup.sh \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/*

WORKDIR $APP_DIR
VOLUME $APP_DIR

EXPOSE ${RAILS_PORT}

CMD '/root/startup.sh'
