# DOCKER
## Задание 1
Установка Docker  
Обновил список пакетов  
```
apt-get update  
```
Установил пакет  
```
apt-get install docker-engine  
```
Добавил утилиту в автозагрузку  
```
systemctl enable --now docker  
```
Установил контейнер hello-world  
```
docker run hello-world  
```
Удалил контейнер hello-world  
```
docker image rm -f hello-world  
```
## Задание 2
Просмотр Docker
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
## Задание 3
Запускаем интерактивную оболочку в контейнере Docker
```
docker exec -it nginx /bin/bash
```
Дальше нам нужен нано поэтосу скачиваем его
```
apt-get update
apt-get install -y nano
```
Далее открываем файл index.html
```
nano /usr/share/nginx/html/index.html
```
В нём меняем заголовок и, по желанию описание
![image](https://github.com/danakahara19/DOCKER/assets/148867574/c6e67777-66b4-4368-b34a-ffc3693e1d8a)
## Задание 4
Создать образ для приложения работающего на фреймворке FastApi








