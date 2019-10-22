# Docker run MySQL+ PHP + Nginx + Redis

- PHP
  - Version: 7.3+
  - Expansions
    - mongodb
    - swoole
    - redis
  - Composer
  - Tool
    - tailf
    - busybox
    - htop
- MYSQL
  - Version: 8.0+
- Redis
  - Version: 4.2
- Nginx
  - Version: alpine

## Quick start

You need to install `docker` first. `https://docs.docker.com/docker-for-windows/install/`

You PC:

```shell
[root@localhost]# git clone git@github.com:zhan3333/nmpr.git
[root@localhost]# cd nmpr
[root@localhost]# docker-compose build --build-arg UNAME=youname UPWD=pwd
[root@localhost]# docker-compose up -d
```

OK! Now you can open `http://localhost`

## Add a virtual host

Docker nginx: add new vhost

```shell
[root@localhost]# cd /work/components/nginx/config/conf.d
[root@localhost]# cp localhost.conf you_vhost.conf
[root@localhost]# vim you_vhost.conf
```

You PC: reload nginx

```shell
[root@localhost]# docker exec nginx /etc/init.d/nginx reload
```

## Config file

- Work dir: `docker-compose.yml`
- MySQL: `./mysql/mysql.cnf`
- Nginx `./work/components/nginx/config/nginx.conf`
- PHP `./work/components/php/config/php.ini`

## Setting

### Use php command in system

## Want to help?

Author: `zhan`

Email to: `grianchan@gmail.com`
