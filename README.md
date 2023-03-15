![image](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
# Реверс-прокси для Telegram-bot на Webhook-ах
Данный проект это веб-сервер Caddy внутри Docker Compose, настроенный в режиме реверс-прокси, используемый для расположения нескольких ботов на одном сервере. SSL-сертификаты автоматически генерируются и обновляются от Let's Encrypt. Конфиг Caddyfile может быть переписан для использования нескольких микросервисов на одном сервере.
## Функционал
* Создание HTTPS-подключения
* Автообновление и создание SSL-сертификатов Let's Encrypt
* Дает возможность расположить несколько ботов или микросервисов на одном сервере
## Инструменты и библиотеки
* Caddy
* Docker
* Docker Compose
## Установка
* Клонировать репозиторий: `git clone https://github.com/LaggerIsME/caddy_for_telegram_bot` 
* Скачать и установить Docker и Docker-Compose: https://docs.docker.com/engine/install/
* Перейти в директорию проекта: `cd ~/caddy_for_telegram_bot`
* Изменить значение переменных в файле `.env`. 
* Создать общую сеть для docker-контейнеров с помощью команды: `docker network create web`
* Проверить создалась ли она с помощью: `docker network ls`
* Запустить реверс-прокси с помощью команды:
* * Linux: `docker compose up -d --build`
* * MacOS, Windows: `docker-compose up -d --build`

Теперь можете запустить своих ботов внутри docker и они будут работать по HTTPS-подключению. 

## Примечания: 
1. Если хотите расположить дополнительного бота, то добавьте еще одну строчку с `proxy_pass {роутер_бота} {имя_контейнера_бота}:{порт бота}` в `Caddyfile`
2. Не забудьте, что в `docker-compose.yml` ВАШЕГО БОТА вы должны будете указать:
```
networks:
  web:
    external: true
```
3. А также добавить все ваши сервисы внутри `docker-compose.yml` ВАШЕГО БОТА в эту сеть:
```
services:
    service_name_1:
        networks:
          - web
    service_name_2:
        networks:
          - web
```
