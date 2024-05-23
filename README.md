# DOCKER
### Задание 1
Установка Docker  
Обновила список пакетов  
```
apt-get update  
```
Установила пакет  
```
apt-get install docker-engine  
```
Добавила утилиту в автозагрузку  
```
systemctl enable --now docker  
```
Установила контейнер hello-world  
```
docker run hello-world  
```
Удалила контейнер hello-world  
```
docker image rm -f hello-world  
```
### Задание 2
Просмотр нашего Docker
```
docker images
```
Просмотр наших контейнеров
```
docker ps
```
пишем команду 
```
docker pull nginx
```
запускаем контейнер
```
docker run --rm -d --anme nginx -v /data/app:/var/www/html -p 0.0.0.0:80:80 nginx
```
заходим на свой айпишник и проверяем 
### Задание 3
Запускаем интерактивную оболочку в контейнере Docker
```
docker exec -it nginx /bin/bash
```
Дальше нам нужен нано поэтосу скачиваем его
```
apt-get update
apt-get install -y nano
```










