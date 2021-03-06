# PHP Laravel environment
Docker environment required to run Laravel (based on official php and mysql docker hub repositories).

[![CircleCI](https://circleci.com/gh/dimadeush/docker-apache-php-laravel.svg?style=svg)](https://circleci.com/gh/dimadeush/docker-apache-php-laravel)

[Source code](https://github.com/dimadeush/docker-apache-php-laravel.git)

## Requirements
* Docker version 18.06 or later
* Docker compose version 1.22 or later
* An editor or IDE
* MySQL Workbench

Note: OS recommendation - Linux Ubuntu based.

## Components:
1. Apache 2.4
2. PHP 7.3 (Apache handler)
3. MySQL 8
4. Laravel 5.7

## Setting up DEV environment
1. Build and start the image from your terminal:
    ```
    docker-compose build
    make start
    make composer-install
    make make env-local
    ```
2. Add domain to local 'hosts' file:
    ```
    127.0.0.1    localhost
    ```
3. Set key for application:
    ```
    make ssh
    php artisan key:generate
    ```
4. Make sure that you have installed migrations/seeds:
    ```
    make migrate
    make seed
    ```
5. Configure Xdebug:
    - In case you need debug only requests from frontend in Firefox:
        * Edit /docker/development/xdebug.ini:
        ```
        xdebug.remote_autostart = 0
        ```
        * Restart container
        * Install locally in Firefox extension "Xdebug helper" and set in settings IDE KEY: PHPSTORM
        * Have fun with debugging
    - In case you need debug any request to an api:
        * Edit /docker/development/xdebug.ini:
        ```
        xdebug.remote_autostart = 1
        ```
        * Restart container
        * Have fun with debugging

## Additional main command available:
    ```
    make start
    make stop
    make restart
    make ssh
    make ssh-supervisord
    make composer-install
    make composer-update
    make info
    make drop-migrate
    make migrate
    make seed
    make phpunit
    etc....
    ```
    Notes: Please see more commands in Makefile

## Architecture & packages
* [Laravel 5.7](https://laravel.com)
* [laravel-migrations-organiser](https://github.com/JayBizzle/Laravel-Migrations-Organiser)
* [phpunit](https://phpunit.de/)
* [phpunit-result-printer](https://github.com/mikeerickson/phpunit-pretty-result-printer)
* [laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)
* [scriptsdev](https://github.com/neronmoon/scriptsdev)

## General guidelines
* **[General](docs/general.md)**

## Working on your project
1. For new feature development, fork `develop` branch into a new branch with one of the two patterns:
    * `feature/{ticketNo}`
2. Commit often, and write descriptive commit messages, so its easier to follow steps taken when reviewing.
3. Push this branch to the repo and create pull request into `develop` to get feedback, with the format `feature/{ticketNo}` - Short descriptive title of Jira task".
4. Iterate as needed.
5. Make sure that "All checks have passed" on circleci and status is green.
6. When PR is approved, it will be squashed & merged, into `develop` and later merged into `release/{No}` for deployment.
