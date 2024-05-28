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
Для начала обратимся к Python для создания нового окружения, которое мы назовём docker
```
pyton3 -m venv docker
```
Открываем его
```
source docker/bin/activate
```
Мы создаём новую директорию, называем её по своему усмотрению и заходим в неё
```
mkdir /fastapi
```
```
cd /fastapi
```
В нём открываем файл requirements.txt, куда мы запишем наши зависимости
```
nano requirements.txt
```
Заполняем его следующим содержимым
```
fastapi>=0.68.0,<0.69.0
pydantic>=1.8.0,<2.0.0
uvicorn>=0.15.0,<0.16.0
```
И устанавливаем зависимости при помощи pip
```
pip install -r requirements.txt
```

В ней создаём директорию app, переходим в неё и создаём 2 файла: __init__.py и main.py. Файл __init__.py оставляем пустым
```
mkdir /fastapi/app
cd /fastapi/app
nano /fastapi/app/__init__.py (сохраняем и выходим сочетаниями клавиш ctrl+s, ctrl+x)
nano /fastapi/app/main.py
```
Заполняем файл main.py следующим образом
```
from typing import Union
```
```
from fastapi import FastAPI
```
```
app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None] = None):
    return {"item_id": item_id, "q": q}
```
Далее в директории /fastapi создаём файл Dockerfile и заполняем его
```
#
FROM python:3.9
#
WORKDIR /code 
#
COPY ./requirements.txt /code/requirements.txt# 
#
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt 
#
COPY ./app /code/app 
#
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
```
Не выходя из директории /fastapi, создаём в ней образ приложения FastAPI
```
docker build -t fastapi /fastapi
```
После прошедшей загрузки запускаем сам контейнер
```
docker run -d --name fastapi -p 80:80 fastapi
```
Чтобы проверить работу контейнера мы должны перейти по ссылке: http://IP_адрес_вашей_машины/items/5?q=somequery Там мы увидим текст на подобии
```
{"item_id": 5, "q": "somequery"}
```
Также нужно ввести и следующую ссылку
```
http://IP_адрес_вашей_машины/docs
```






