# sp3ber_microservices
sp3ber microservices repository

[![Build Status](https://travis-ci.com/otus-devops-2019-05/sp3ber_microservices.svg?branch=master)](https://travis-ci.com/otus-devops-2019-05/sp3ber_infra)

## Домашние задания

[Технологии контенеризации. Введение в Docker](#docker_2)

[Docker образы. Микросервисы](#docker_3)

[Docker networks. Docker-compose](#docker_4)

[Устройство Gitlab CI](#gitlab_ci)

[Системы мониторинга](#monitoring_1)

[Мониторинг приложения и инфраструктуры](#monitoring_2)

[Логирование и распределенная трассировка](#logging_1)

<a name="#docker_2"><h4>Технологии контенеризации. Введение в Docker</h4></a>

<h5>Что сделано:</h3>
- Добавил описание результата локального исполнения команды docker images
- Добавил описание различий образа и контейнера на основе результата вывода docker inspect (для образа и контейнера)
- Создал docker host (удаленно и локально)
- Создал свой образ
- Поработал с Docker Hub, docker-machine


<a name="#docker_3"><h4>Docker образы. Микросервисы</h4></a>

<h5>Что сделано:</h3>
- Описал и собрал Docker-образы для сервисного приложения
- Попроболвал оптимизировать работу с Docker-образами (ui образ)
- Научился ипользовать network aliases (для bridge), volumes. Пример с собственными алиасами:
<pre>
    docker run -d --network=reddit --network-alias=reddit_post_db --network-alias=reddit_comment_db mongo:latest
    docker run -d -e POST_DATABASE_HOST="reddit_post_db" --network=reddit --network-alias=reddit_post sp3ber/post:1.0
    docker run -d -e COMMENT_DATABASE_HOST="reddit_comment_db" --network=reddit --network-alias=reddit_comment sp3ber/comment:1.0
    docker run -d -e POST_SERVICE_HOST="reddit_post" -e COMMENT_SERVICE_HOST="reddit_comment" --network=reddit -p 9292:9292 sp3ber/ui:1.0
</pre>

<a name="#docker_4"><h4>Docker networks. Docker</h4></a>

<h5>Что сделано:</h3>
- Разобрался с разными docker networks (none, host, bridge)
- Собрал и запустил образы с помощью docker-compose
- Параметризировал образы, собираемые в docker-compose, с помощью env переменных из .env файла
- Разобрался с дефолтной схемой формирования docker образа, создаваемого с помощью docker-compose:
<pre>
    Дефолтная схема формирования имени - project_service_index (где project и service в нашем случае просто подкаталоги, а index - номер инстанса - т.к. мы не скейлим ничего, то всех инстансов по одному), но имя можно задать самому через поле container_name
</pre>

<a name="#gitlab_ci"><h4>Устройство Gitlab CI</h4></a>

<h5>Что сделано:</h3>
- Подготовил инсталляцию Gitlab CI
- Подготовил репозиторий с кодом приложения
- Описал для приложения этапы пайплайна
- Определил окружения
- Добавил интеграцию с gitlab в слаке (ссылка на канал https://devops-team-otus.slack.com/messages/CKE4BLG49)

<a name="#monitoring_1"><h4>Системы мониторинга</h4></a>

<h5>Что сделано:</h3>
- Познакомился с Prometheus: запуск, конфигурация, знакомство с Web UI
- Добавил мониторинг состояния микросервисов
- Добавил сбор метрик хоста с использованием экспортера (node-exporter)
- Опубликова образы микросервисов и прометея - https://cloud.docker.com/u/sp3ber/repository/list

<a name="#monitoring_2"><h4>Мониторинг приложения и инфраструктуры</h4></a>

<h5>Что сделано:</h3>
- Добавлен мониторинг Docker контейнеров
- Добавлена визуализация метрик (grafana)
- Добавлен сбор метрик работы приложения и бизнес метрик
- Настроен и проверен  алертинга
- Опубликован образ алерт-менеджера - https://cloud.docker.com/u/sp3ber/repository/list

<a name="#logging_1"><h4>Логирование и распределенная трассировка</h4></a>

<h5>Что сделано:</h3>
- настроен сбор структурированных и неструктурированных логов из сервисов ui и post
- добавлена Kibana для визуализации логов
- добавлена распределенная трасировка через zipkin
