FROM ruby:3.2.2

ENV APP_ROOT /myapp

RUN mkdir $APP_ROOT

WORKDIR $APP_ROOT

COPY docker/deploy/production/entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh

COPY Gemfile $APP_ROOT/Gemfile
COPY Gemfile.lock $APP_ROOT/Gemfile.lock

RUN apt-get update -qq \
    && apt-get install -y build-essential libpq-dev \
    && bundle config set --local without 'development test' \
    && bundle install

COPY . $APP_ROOT

ENTRYPOINT ["entrypoint.sh"]

EXPOSE 3002
