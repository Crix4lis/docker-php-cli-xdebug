
> author: Michał Powała <br>
> source repository: [docker-php-cli-xdebug](https://github.com/Crix4lis/docker-php-cli-xdebug)

# docker-php-cli-xdebug

This repository contains running PHP CLI docker image with slightly extended [official php imgage](https://hub.docker.com/r/_/php/). It's extended with configured xDebug extension and installed Composer. The repostory is useful as basic image for any PHP application. Use Composer to download needed dependencies, libraries or PHP frameworks like Symfony.

## HOW TO USE IT
1. Install Docker: [OFFICIAL INSTRUCTION](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository)
1. Install Compose: [OFFICIAL INSTRUCTION](https://docs.docker.com/compose/install/#install-compose)
1. Change directory to dir you cloned the repo and type: `docker-compose up -d`
1. Enter the container: `docker-compose exec cli bash`
1. Turn on and turn off debugging mode with: `xdebugstart` and `xdebugstop`
1. Run your script with: php your_script.php

## HOW TO SET UP YOUR PHPSTORM IDE
1. Go to options
1. Go to Languages & Frameworks > PHP > Debug
1. Scroll down to "Xdebug" section
1. Make sure:
    - Debug port is set to: `9000`
    - Can accept external connections is set to: `checked`
1. Go to Languages & Frameworks > PHP > Servers and set up:
    - Name: `docker-xdebug-server`
    - Host: does not matter
    - Port: does not matter
    - Debugger: `Xdebug`
    - Use path mappings: `checked`
    - Absolute path on the server: `/volume`

> DON'T FORGET: to start listening for PHP Debug connections in the IDE: <br>
![Start Listening for PHP Debug connections picture](https://cdn.deliciousbrains.com/content/uploads/2017/02/07162817/script-147_js_-_wp-migrate-db-pro_-____PLUGINS_wp-migrate-db-pro_.png "Listen for Debug connections")

## HOW TO TURN ON AND TURN OFF XDEBUG SESSION
Inside docker container type (via bash):
- To turn on: `xdebugstart`
- To turn off: `xdebugstop`
