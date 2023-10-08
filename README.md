# Cоциальная сеть для обмена фотографиями любимых питомцев.

## Описание проекта.

Проект состоит из бэкенд-приложения на Django и фронтенд-приложения на React и представляет собой незамысловатый [сайт](https://kittygramoksiasti.ddns.net/), на котором пользователи могут зарегистрироваться и авторизоваться, добавить нового котика на сайт или изменить существующего (кличку, описание, фото и т.п.), а также просмотреть записи других пользователей. 

Основной упор при реализации данного проекта делался на отработку запуска проекта в контейнерах на облачном сервере и настройки CI/CD (автоматическое тестирование и деплой проекта на удалённый сервер).
Автоматизация настроена с помощью сервиса GitHub Actions: при пуше в ветку main проект тестируется, в случае успешного прохождения тестов образы обновлятся на Docker Hub, на удаленном сервере запускаются контейнеры из обновлённых образов.
После успешного деплоя приходит сообщение в Телеграм.

## Технологии

 - Python 3.9
 - Django==3.2.3
 - djangorestframework==3.12.4
 - Gunicorn
 - Nginx
 - React


## Запуск проекта из образов с Docker hub
Для запуска необходимо на сервере создать папку проекта, например kittygram, и перейти в нее:
```
mkdir kittygram
cd kittygram
```

В папку проекта скачиваем файл docker-compose.production.yml и запускаем его:
```
sudo docker compose -f docker-compose.production.yml up
```
Произойдет скачивание образов, создание и включение контейнеров, создание томов и сети.

И далее проект доступен на: https://kittygramoksiasti.ddns.net/

## Запуск проекта из репозитория GitHub
Клонируем себе репозиторий:
```
git clone git@github.com:OksanaAstashkina/kittygram_final.git
```

Выполняем запуск:
```
sudo docker compose -f docker-compose.yml up
```

После запуска необходимо выполнить сбор статистики и миграции бэкенда. Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается.

```
sudo docker compose -f docker-compose.yml exec backend python manage.py migrate

sudo docker compose -f docker-compose.yml exec backend python manage.py collectstatic

sudo docker compose -f docker-compose.yml exec backend cp -r /app/collected_static/. /backend_static/static/
```

А далее проект доступен на: http://localhost:9000/

## Остановка оркестра контейнеров

В окне, где был запуск Ctrl+С или в другом окне:
```
sudo docker compose -f [имя-файла-docker-compose.yml] down
```

***
## *Автор*
Оксана Асташкина - [GitHub](https://github.com/OksanaAstashkina)

### *Дата создания*
Март, 2023 г.
