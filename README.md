# sp3ber_microservices
sp3ber microservices repository

[![Build Status](https://travis-ci.com/otus-devops-2019-05/sp3ber_microservices.svg?branch=master)](https://travis-ci.com/otus-devops-2019-05/sp3ber_infra)

## Домашние задания

[Технологии контенеризации. Введение в Docker](#docker_2)

[Docker образы. Микросервисы](#docker_3)

[Docker networks. Docker-compose](#docker_4)

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
