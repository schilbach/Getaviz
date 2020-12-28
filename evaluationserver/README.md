# README

The evaluation server is a rails application capable to support the evaluation of websites. Currently its main use is the evaluation of x3dom software visualizations.  

## Features

* administration of different experiments
* creation of different question types
* random assignment of participants to different scenes
* export of results
* login only required fpr administrative functions


## Setup ##


* install podman
* podman build . -f Dockerfile.development -t evalserver-dev:0.0.1
* mkdir -p ./db-data
* touch .docker_bash_history
* podman pod create --name eval-server-development -p 54321:3000
* podman run -d --restart=always --pod=eval-server-development --volume=./db-data:/var/lib/postgresql/main/:Z  -e POSTGRES_DB="eval_server_development" -e POSTGRES_USER="jasch" -e POSTGRES_PASSWORD="none" --name=evalserver-db  postgres:13.1
* podman run -d -it --name=evalserver-rails --pod=eval-server-development --volume=.:/app:Z --volume=.docker_bash_history:/root/.bash_history:Z evalserver-dev:0.0.1
* podman run -d -it --name=evalserver-rails-webpack --pod=eval-server-development --volume=.:/app:Z evalserver-dev:0.0.1 /app/bin/webpack-dev-server
* podman exec -it evalserver-rails  /bin/bash





<!--
#### manual setup ####-->
<!--
* install Ruby in version 2.0 or above (along with ruby, bundler, rake)
* install mySQL oder equivalent drop-in-replacement (e.g. MariaDB)
* create mySQL user
* git clone
* create source.sh in main directory with creddentials for mysql-database to for config/database.yml
* bundle install
* bundle exec rake db:create
* bundle exec rake db:migrate
* bundle exec rails server -p [port]
-->
