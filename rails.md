# rails get stalled because of spring

DISABLE_SPRING=1 rails generate devise:install

To check if the problem comes from spring :
spring stop
rails generate

# kill a rails server

lsof -wni tcp:3000

# Make a gem for the 1st time

https://www.sodifrance.fr/blog/creer-et-publier-une-gem-ruby/
@pblayo on rubygems.org

# Docker

## Dockerfile

```
FROM ruby:2.5
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client
RUN mkdir /myapp
WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install
COPY . /myapp

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]
```

## Gemfile

It’ll be overwritten in a moment by rails new.

```
source 'https://rubygems.org'
gem 'rails', '~>5'
```

Create an empty Gemfile.lock to build our Dockerfile.

```
touch Gemfile.lock
```

## entrypoint.sh

Next, provide an entrypoint script to fix a Rails-specific issue that prevents the server from restarting when a certain server.pid file pre-exists. This script will be executed every time the container gets started. entrypoint.sh consists of:

```
#!/bin/bash
set -e

# Remove a potentially pre-existing server.pid for Rails.
rm -f /myapp/tmp/pids/server.pid

# Then exec the container's main process (what's set as CMD in the Dockerfile).
exec "$@"
```

## docker-compose.yml

```
version: '3'
services:
  db:
    image: postgres
    volumes:
      - ./tmp/db:/var/lib/postgresql/data
  web:
    build: .
    command: bash -c "rm -f tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    volumes:
      - .:/myapp
    ports:
      - "3000:3000"
    depends_on:
      - db
```

```
docker-compose run web rails new . --force --no-deps --database=postgresql
sudo chown -R $USER:$USER .
docker-compose build
```

Replace the contents of config/database.yml with the following:

```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```


```
docker-compose up
docker-compose run web rake db:create
```

From https://docs.docker.com/compose/rails/

# bootstrap

To have boostrap work, in `Dockerfile` I then needed to replace
```
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client
```

with

```
# https://github.com/nodesource/distributions#installation-instructions
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
        && apt-get install -y nodejs
```

update_all
