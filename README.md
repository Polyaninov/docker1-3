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




3 Написать Dockerfile для собственной версии nginx:
удалить конфиг по умолчанию (default)
создать конфиг файл для статического сайта, расположенного в /var/www/landing
установить в image:
vim
iputils-ping
iproute2
dnsutils
установить таймзону Europe/Moscow
изменить пользователя в главном конифге nginx на www-data
в директорию /etc/nginx положить файл deny.conf
location ~ /\.ht {
    return 404;
}
location ~ /\.svn {
    return 404;
}
location ~ /\.git {
    return 404;
}
location ~ /web.config {
    return 404;
}
в директорию /var/www/landing положить файлы из репозитория https://github.com/AnastasiyaGapochkina01/book-landing/tree/main/book
Запустить из собранного image контейнер и проверить его работоспособность - при запросе должен отдаваться похожий на это https://themes.3rdwavemedia.com/demo/bs5/devbook/ лендинг


sudo docker build -t my-nginx . 
