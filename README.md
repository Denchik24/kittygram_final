
# Kittygram - сервис для любителей котиков.
<div id="header" align="left">  <img src="https://99px.ru/sstorage/86/2023/03/image_86160323111137975234.gif" width="200"/> </div>

![workflow](https://github.com/Denchik24/kittygram_final/actions/workflows/main.yml/badge.svg)

## Технологии
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=blue) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB) ![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white) ![Gunicorn](https://img.shields.io/badge/gunicorn-%298729.svg?style=for-the-badge&logo=gunicorn&logoColor=white) ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)

___
##   Что умеет проект:
Добавлять, просматривать, редактировать и удалять котиков. Добавлять новые и присваивать уже существующие достижения. Просматривать чужих котов и их достижения. 

##   Установка 
Клонируйте репозиторий на свой компьютер:
git clone git@github.com:Denchik24/kittygram_final.git cd kittygram Создайте файл .env и заполните его своими данными. Перечень данных указан в корневой директории проекта в файле .env.example.

##   Создание Docker-образов 
Замените username на ваш логин на DockerHub:
имя пользователя для сборки внешнего интерфейса docker /kittygram_frontend . cd ../ имя пользователя для сборки внутреннего интерфейса docker/kittygram_backend . cd ../ имя пользователя для сборки nginx docker /kittygram_gateway.
Загрузите образы на DockerHub:
docker push username/kittygram_frontend docker push username/kittygram_backend docker push username/kittygram_gateway 

##  Деплой на сервере Подключитесь к удаленному серверу
ssh -i путь_до_файла_с_SSH_ключом/название_файла_с_SSH_ключом имя_пользователя@ip_адрес_сервера 
Создайте на сервере директорию kittygram через терминал
mkdir kittygram 

##   Установка docker compose на сервер:
sudo apt update sudo apt install curl curl -fSL https://get.docker.com -o get-docker.sh sudo sh ./get-docker.sh sudo apt-get install docker-compose-plugin
В директорию kittygram/ скопируйте файлы docker-compose.production.yml и .env:
scp -i path_to_SSH/SSH_name docker-compose.production.yml username@server_ip:/home/username/kittygram/docker-compose.production.yml
ath_to_SSH — путь к файлу с SSH-ключом;
SSH_name — имя файла с SSH-ключом (без расширения);
username — ваше имя пользователя на сервере;
server_ip — IP вашего сервера. 
Запустите docker compose в режиме демона:
создание sudo docker -f docker-compose.production.yml up -d 
Выполните миграции, соберите статические файлы бэкенда и скопируйте их в /backend_static/static/:
sudo docker compose -f docker-compose.production.серверная часть yml exec на python manage.py
перенесите sudo docker compose -f docker-compose.production.серверная часть yml exec на python manage.py 
соберите статический sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/ 
На сервере в редакторе nano откройте конфиг Nginx:
sudo nano /etc/nginx/sites-enabled/default 
Измените настройки location в секции server:
location / { proxy_set_header Host $http_host; proxy_pass http://127.0.0.1:9000; } 
Проверьте работоспособность конфига Nginx:
sudo nginx -t Если ответ в терминале такой, значит, ошибок нет:
nginx: синтаксис файла конфигурации /etc/nginx/nginx.conf в порядке nginx: тест файла конфигурации /etc /nginx /nginx.conf выполнен успешно 
Перезапускаем Nginx
sudo service nginx reload

##  Настройка CI/CD 
Файл workflow уже написан. Он находится в директории kittygram/.github/workflows/main.yml Для адаптации его на своем сервере добавьте секреты в GitHub Actions:
DOCKER_USERNAME # имя пользователя в DockerHub
DOCKER_PASSWORD # пароль пользователя в DockerHub 
HOST # ip_address сервера 
USER # имя пользователя 
SSH_KEY # приватный ssh-ключ (cat ~/.ssh/id_rsa)
SSH_PASSPHRASE # кодовая фраза (пароль) для ssh-ключа
TELEGRAM_TO # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start) 
TELEGRAM_TOKEN # токен бота (получить токен можно у @BotFather, /token, имя бота

Автор Денис Сазонов
