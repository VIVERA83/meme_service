# Mem Center 

___
<span id="0"></span>

### <span id="1">1. </span><span style="color:purple">Описание</span>

 В этом сервисе можно сгенерировать «быстрый мем». 

### <span id="2">2. </span><span style="color:purple">Служебные команды для запуска</span> 


Запуск приложения в docker контейнере
Перед запуском приложения в контейнере необходимо создать:
1. __.env__ - за основу можно взять [.env_example](.env_example)
2. __.env_image_store__ - за основу можно взять [env_example_image_store](env_example_image_store)
3. __.env_meme_center__ - за основу можно взять [env_example_meme_center](env_example_meme_center)

__Далее выполняем команду:__ 

```bash
docker compose up --build
```
__Теперь необходимо создать необходимые БД в Postgres. для это выполняем следующие действия
1. за ходим в контейнер [meme_center](meme_center)
```bash
docker exec -it meme_center bash
```
```bash
cd meme_center 
alembic init -t async alembic
```
```bash
cd meme_center 
alembic revision --autogenerate -m "Initial tables"
```
```bash
cd meme_center
alembic upgrade head
```