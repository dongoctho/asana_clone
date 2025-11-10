## Generate SSL certificate

mkdir -p docker/ssl
openssl req -new -x509 -days 365 -nodes \
  -out docker/ssl/localhost.crt \
  -keyout docker/ssl/localhost.key

## Install composer

Composer install