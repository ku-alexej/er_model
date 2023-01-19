# er_model

[The link to ER-model](https://app.quickdatabasediagrams.com/#/d/FaHQNw)

Пример запроса названий топ-10 фильмов по лайкам.

SELECT name.films
FROM films
WHERE film_id IN (SELECT film_id.likes
                  FROM likes
                  GROUP BY film_id
                  ORDER BY SUM(user_id) DESC
                  LIMIT 10);
