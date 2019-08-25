# Devilbox

Allows you to have an unlimited about of projects ready without having to configure any virtualhosts

## Prerequisites

The only prerequisites needed is a valid docker install and docker-compose

## Installation

1. Download devilbox
    `git clone https://github.com/cytopia/devilbox`
2. Create a .env file
  Copy the example env file to .env
    `cp env-example .env`
3. Set the UID and GID to your current user's UID and GID

## Start the Devilbox

* To start all containers -- `docker-compose up`
* To start all containers in the background -- `docker-compose up -d`
* To start some containers -- `docker-compose up -d httpd php mysql`

## Stop the Devilbox

* Stop all containers -- `docker-compose stop`
* Remove stopped containers -- `docker-compose rm -f`

## Open the intranet

* In a browser, go to http://127.0.0.1 (or http://localhost) -- this will show all running and stopped containers

## WordPress Install

1. Start the devilbox -- `docker-compose up -d php mysql httpd`
2. Enter the PHP container -- `./shell`
3. Create a new vhost directory -- `mkdir <vhost_name>
4. Download WordPress -- `cd <vhost_name> && git clone https://github.com/WordPress/WordPress wordpress.git`
5. Symlink webroot -- `ln -s wordpress.git/ htdocs`
6. Add MySQL Database -- `mysql -u root -h 127.0.0.1 -p -e 'CREATE DATABASE <vhost_name>'`
7. Add vhost name to /etc/hosts -- `127.0.0.1 <vhost_name>.loc`
8. Open vhost in browser and complete install steps
