1. Написать Dockerfile для запуска в docker кода на php

FROM php:8.0-apache
COPY index.php /var/www/html/index.php
WORKDIR /var/www/html
EXPOSE 80
CMD [ "apache2-foreground" ]

   
<?php
phpinfo();
?>
Note

В качестве базового image можно взять php:8.0-apache.
docker build -t my-php-app .

Запустить из собранного image контейнер и проверить его работоспособность

sudo docker run -d -p 8080:80 my-php-app 
curl 127.0.0.1:8080


2. Написать Dockerfile для приложения https://github.com/AnastasiyaGapochkina01/node-app, запустить из собранного image контейнер и проверить его работоспособность

FROM node:16
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]




curl 127.0.0.1:3000
