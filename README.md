1. Введение в Docker

Docker — это платформа для создания, развертывания и управления контейнерами. Контейнеры представляют собой легковесные, изолированные среды для запуска приложений.

Основные понятия:

Контейнер: изолированная среда, которая содержит приложение и его зависимости.

Образ (Image): шаблон для создания контейнера. Образы неизменяемы и состоят из слоёв.

Docker Engine: движок, обеспечивающий выполнение контейнеров.

Docker Hub: облачная платформа для хранения и обмена образами.

2. Установка Docker

Шаги установки:

Зайдите на официальный сайт Docker (https://www.docker.com) и выберите версию для вашей операционной системы.

Установите Docker Desktop (Windows, macOS) или Docker Engine (Linux).

Проверьте установку командой:

docker --version

3. Основные команды Docker

Образы:

docker pull <image> — загрузить образ.

docker images — список загруженных образов.

docker rmi <image> — удалить образ.

Контейнеры:

docker run <image> — запустить контейнер.

docker ps — список запущенных контейнеров.

docker ps -a — список всех контейнеров.

docker stop <container> — остановить контейнер.

docker rm <container> — удалить контейнер.

Работа с логами:

docker logs <container> — просмотреть логи.

Интерактивный доступ:

docker exec -it <container> bash — подключиться к контейнеру.

4. Dockerfile

Dockerfile — это текстовый файл с инструкциями для создания образа.

Пример Dockerfile:

# Используем базовый образ
FROM python:3.9

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем файлы
COPY . /app

# Устанавливаем зависимости
RUN pip install -r requirements.txt

# Указываем команду для запуска контейнера
CMD ["python", "app.py"]

Основные инструкции Dockerfile:

FROM — базовый образ.

COPY — копирование файлов.

RUN — выполнение команды при создании образа.

CMD — команда, выполняемая при старте контейнера.

5. Docker Compose

Docker Compose — инструмент для управления несколькими контейнерами с помощью одного файла docker-compose.yml.

Пример docker-compose.yml:

version: '3.8'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  app:
    build:
      context: ./app
    volumes:
      - ./app:/app
    depends_on:
      - db
  db:
    image: postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password

Основные команды Docker Compose:

docker-compose up — запустить контейнеры.

docker-compose down — остановить контейнеры.

6. Сетевые возможности Docker

Docker предоставляет встроенные механизмы для работы с сетью:

Bridge — стандартная сеть для контейнеров на одном хосте.

Host — контейнер использует сеть хоста.

Overlay — для работы контейнеров на разных хостах.

Команды для управления сетью:

docker network ls — список сетей.

docker network create <name> — создать сеть.

docker network connect <network> <container> — подключить контейнер к сети.

7. Хранение данных (Volumes)

Для хранения данных, которые должны сохраняться после остановки контейнера, используются Volumes.

Основные команды:

docker volume create <name> — создать том.

docker volume ls — список томов.

docker volume rm <name> — удалить том.

Пример использования в docker-compose.yml:

services:
  db:
    image: postgres
    volumes:
      - db_data:/var/lib/postgresql/data
volumes:
  db_data:

8. Лучшие практики

Минимизируйте размер образов, используя легковесные базовые образы (например, alpine).

Используйте .dockerignore для исключения ненужных файлов при сборке.

Не храните конфиденциальные данные в Dockerfile — используйте переменные окружения.

Регулярно обновляйте образы для устранения уязвимостей.

9. Полезные ресурсы

Официальная документация Docker

Docker Hub

