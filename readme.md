# Docker run MySQL+ PHP + Nginx + Redis

- PHP
  - Version: 7.3+
  - Expansions
  - Redis
  - Composer
- MYSQL
  - Version: 8.0+
- Redis
  - Version: 4.2
- Nginx
  - Version: alpine

## Quick start

You need to install `docker` first. `https://docs.docker.com/docker-for-windows/install/`

1. down `git clone git@github.com:zhan3333/nmpr.git`
2. cd `cd nmpr`
3. build `docker-compose build`
4. up `docker-compose up -d`
5. Browser access `http://localhost`

## Add a virtual host

1. `cp /work/components/nginx/config/conf.d/localhost.conf /work/components/nginx/config/conf.d/you_host.conf`
2. `vim you_host.conf`
3. `docker exec nginx /etc/init.d/nginx reload`

## Config file

- Work dir: `docker-compose.yml`
- MYSQL: `./mysql/mysql.cnf`
- NGINX `./work/components/nginx/config/nginx.conf`
- PHP `./work/components/php/config/php.ini`

## Setting

### Use php command in system

1. Windows
Add this dir to system user path (use php.bat)

2. Linux
Add php file to `/usr/local/php`

## Want to help?

Email to: `grianchan@gmail.com`
