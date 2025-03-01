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
