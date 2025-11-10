## Generate SSL certificate

mkdir -p docker/ssl

openssl req -new -x509 -days 365 -nodes -out docker/ssl/localhost.crt -keyout docker/ssl/localhost.key

## Run docker-compose

docker-compose up -d --build

## Install composer

composer install