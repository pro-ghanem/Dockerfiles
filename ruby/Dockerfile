FROM ruby:2.7.2
# Use a directory called /code in which to store
# this application's files. (The directory name
# is arbitrary and could have been anything.)
WORKDIR /app
# Copy all the application's files into the /code
# directory.
COPY . /app
# Run bundle install to install the Ruby dependencies.
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN bundle install
# Install Yarn.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn
ARG PG_MAJOR=13
ARG NODE_MAJOR=14
ARG BUNDLER_VERSION=2.2.5
ARG YARN_VERSION=1.22.5
# Common dependencies
RUN apt-get update -qq \
  && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    build-essential \
    gnupg2 \
    curl \
    less \
    vim \
    git \
    python-dev \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && truncate -s 0 /var/log/*log
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
# Add PostgreSQL to sources list
RUN curl -sSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && echo 'deb http://apt.postgresql.org/pub/repos/apt/ buster-pgdg main' $PG_MAJOR > /etc/apt/sources.list.d/pgdg.list
# Add NodeJS to sources list
RUN curl -sL https://deb.nodesource.com/setup_$NODE_MAJOR.x | bash -
# Add Yarn to the sources list
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo 'deb http://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list
# Install dependencies
COPY .dockerdev/Aptfile /tmp/Aptfile
RUN apt-get update -qq && DEBIAN_FRONTEND=noninteractive apt-get -yq dist-upgrade && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    libpq-dev \
    postgresql-client-$PG_MAJOR \
    nodejs \
    yarn=$YARN_VERSION-1 \
    $(cat /tmp/Aptfile | xargs) && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    truncate -s 0 /var/log/*log
# Configure bundler
ENV LANG=C.UTF-8 \
  BUNDLE_JOBS=4 \
  BUNDLE_RETRY=3 \
  BUNDLE_APP_CONFIG=.bundle
# Upgrade RubyGems and install required Bundler version
RUN gem update --system && \
    gem install bundler:$BUNDLER_VERSION
# Run binstubs without prefixing with `bin/` or `bundle exec`
ENV PATH /app/bin:$PATH
# Create a directory for the app code
RUN mkdir -p /app
WORKDIR /app
COPY . /app
# backend env
ENV NODE_ENV=development \
  RAILS_ENV=development \
  WEBPACKER_DEV_SERVER_HOST=0.0.0.0 \
  NODE_ENV=development \
  RAILS_ENV=development \
  REDIS_URL=redis://redis-master:6379 \
  DATABASE_URL=postgres://postgres:superfoods@postgres:5432 \
  BOOTSNAP_CACHE_DIR=/usr/local/bundle/_bootsnap \
  WEBPACKER_DEV_SERVER_HOST=webpacker \
  WEB_CONCURRENCY=1 \
  HISTFILE=/app/log/.bash_history \
  PSQL_HISTFILE=/app/log/.psql_history \
  EDITOR=vi
# Run yarn install to install JavaScript dependencies.
#RUN yarn install --check-files
# Set "rails server -b 0.0.0.0" as the command to
# run when this container starts.
# RUN bundle exec rails server -e production -p 3000
# CMD ["rails", "server", "-b", "0.0.0.0"]    # u can use it but i want to run many commands at statrtup so i will use entrypoint.sh
CMD ["/app/entrypoint.sh"]
