# Docker run mysql + php + nginx + redis

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

1. build `docker-compose build`
2. up `docker-compose up -d`
3. Browser access `http://localhost`

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

### Cache

### Use in vscode

- Windows
  - `"php.executablePath": "nmpr-path\\php.bat"`

## Want to help?

Email to: `grianchan@gmail.com`