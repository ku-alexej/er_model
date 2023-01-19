# ER_model

Диаграмма отражает связи таблиц для хранения данных приложения Filmorate.

[The link to ER-model](https://app.quickdatabasediagrams.com/#/d/FaHQNw)

## Таблицы
 
**```Films```**

Содержит данные о фильмах.
- Первичный ключ ```Film_Id``` - идентификатор фильма;
- ```Name``` - название фильма;
- ```Description``` - описание фильма (макс 200 символов);
- ```Release_Date``` - дата выхода;
- ```Duration``` - продолжительность фильма в минутах;
- ```Rate_Id``` - идентификатор возрастного рейтинга.
 
**```Films_Genres```**

Содержит жанры фильмов.
- Первичный ключ ```Films_Genre_Id``` - идентификатор в таблице;
- ```Film_Id``` - идентификатор фильма;
- ```Genre_Id``` - идентификатор жанра.
 
**```Genres```**

Содержит названия жанров фильмов.
- Первичный ключ ```Genre_Id``` - идентификатор жанра;
- ```Genre_Name``` - название жанра.
 
**```Rates```**

Содержит возрастные рейтинги фильмов.
- Первичный ключ ```Rate_Id``` - идентификатор рейтиинга;
- ```Rate_Name``` - название рейтинга.
 
**```Users```**

Содержит данные пользователей.
- Первичный ключ ```User_Id``` - идентификатор пользователя;
- ```Email``` - электронная почта пользователя (уникальное значение);
- ```Login``` - логин пользователя (уникальное значение);
- ```Name``` - имя пользователя;
- ```Birthday``` - дата рождения пользователя.
 
**```Likes```**

Содержит данные о понравившихся фильмах.
- Первичный ключ ```Like_Id``` - идентификатор в таблице оставленного лайка;
- ```Film_Id``` - идентификатор фильма;
- ```User_Id``` - идентификатор пользователя, поставившего лайл.
 
**```Friends```**

Содержит данные о дружбе пользователей.
- Первичный ключ ```Request_Id``` - идентификатор в таблице запроса на дружбу;
- ```User_Id``` - идентификатор пользователя отправившего запрос на дружбу;
- ```Friend_Id``` - идентификатор пользователя получившего запрос на дружбу.
 
## Пример запроса названий топ-10 фильмов по лайкам.

```
SELECT name.films
FROM films
WHERE film_id IN (SELECT film_id.likes
                  FROM likes
                  GROUP BY film_id
                  ORDER BY SUM(user_id) DESC
                  LIMIT 10);
```
