## Ambiente de trabajo para trabajar laravel + docker 


Requesitos del sistema:

Docker instalado
Docker compose  instalado

Para mac Descargar desde el sitio oficial y instalar dmg

para linux dejo unos link de apoyo para la instalacion en ubuntu 18-04

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04
https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04


Luego de tener instalado ambos se debe ejecutar lo siguiente:

docker-composer up -d

En el caso de errores con puertos en uso verifica los siguientes puertos esten libres:

3307 /Mysql
80 /Nginx
6379 /Redis
9000 /php-fpm

Para instalar laravel atraves de composer 

docker-compose exec app composer create-project --prefer-dist laravel/laravel .

Instalar dependendia predis para redis
docker-compose exec app composer require predis/predis

configurar .env esta es la configuracion que yo use para este ejemplo.

APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:IjdxBpuJy6D7shiydbigj7LwDeAAEOKMXrLLKzvpaJo=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=local

BROADCAST_DRIVER=log
CACHE_DRIVER=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis
SESSION_LIFETIME=120

REDIS_HOST=redis
REDIS_PASSWORD=dpjJgWKNPSmLVX9sNKHhZCzN5QcnVnSd
REDIS_PORT=6379

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=mt1

MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"


crea auth
docker-compose exec app php artisan make:auth

realizar mmigracion de las tablas auth
docker-compose exec app php artisan migrate
