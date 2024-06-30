# Meme Service

___
<span id="0"></span>

### <span id="1">1. </span><span style="color:purple">Описание</span>

Meme Service - сервис для работы с МЕМАМИ обеспечивает удобное хранение и выемку по необходимости.
А вообще это небольшое тестовое задание в котором необходимо было реализовать приложение на основе микро сервисной
архитектуры. Задача была создать интерфейс для взаимодействия с внешними запросами. В данной
роли [mem_api](https://github.com/VIVERA83/mem_api/tree/master).
Принимает картинку и подпись к ней, подпись закидывает в БД Postgres, а картинку в хранилище S3, в нашем случае
[Minio](https://min.io/docs/minio/linux/index.html). Для работы с хранящем было указано сделать отдельный
сервис. В роли такого сервиса [meme_storage](https://github.com/VIVERA83/meme_storage/tree/master). В целом возможные
действия с данными выглядят так:

1. Добавление нового (картинка + подпись)
2. Посмотреть все записи с использованием пагинации
3. Обновить данные, можно заменить картинку или изменить текст либо все сразу
4. Удалить данные, данные удаляются как в БД так и В хранилище

При запуске приложения доступ к Swagger осуществляется по ссылке http://127.0.0.1:8000/docs при условии что данные для
переменных окружения взяты из примера.

Реализована небольшая валидация данных и обработка возможных ошибок:

1. Есть ограничения по размеру и типу файла, поддерживаем пока только jpg.
2. Если запрашиваемого мема нет или данные не полные выводится соответствующая ошибка

### <span id="2">2. </span><span style="color:purple">Запуск с помощью Docker</span>

Самый простой вариант запуска.

Перед запуском приложения необходимо создать:

1. __.env__ - Для [docker-compose.yml](docker-compose.yml) в корневом каталоге. За основу можно
   взять [.env_example](.env_example)
2. __.env__ - Для [mem_api](https://github.com/VIVERA83/mem_api/tree/master) в одноименном каталоге за основу можно
   взять [.env_example](https://github.com/VIVERA83/mem_api/blob/master/.env_example)
3. __.env__ - Для [meme_storage](https://github.com/VIVERA83/meme_storage/tree/master) в одноименном каталоге за основу
   можно
   взять [.env_example](https://github.com/VIVERA83/meme_storage/blob/master/.env_example)

__Далее выполняем команду:__

```bash
docker compose up --build
```

Собственно всё залетаем на http://127.0.0.1:8000/docs и тыркаемся.

### <span id="3">3. </span><span style="color:purple">Тесты...</span>

1. Для запуска тестов нужно в [docker-compose.yml](docker-compose.yml) снять комментарии со всех строк(они открывают
   порты)
2. Запускаем все в контейнере

```bash
docker compose up --build
```

3. Переходим в корень
   папки [tests](https://github.com/VIVERA83/mem_api/tree/677b8d4963fb5debc05386c1054f42537fde043c/tests) и выполняем
   миграцию (создаем тестовую БД)
   Тоже нужно создать __.env__ файл пример там же.

```bash
alembic upgrade head
```

4. Запускаем тесты (предварительно необходимо установить необходимые зависимости которые находятся
   в [requirements.txt](https://github.com/VIVERA83/mem_api/blob/677b8d4963fb5debc05386c1054f42537fde043c/requirements.txt))

```bash
pytest
```
