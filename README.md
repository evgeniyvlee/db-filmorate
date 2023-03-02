# db-filmorate
DB scheme for filmorate app

> Вывести 10 популярных фильмов

```sql
SELECT
  f.name AS film_name,
  COUNT(l.id) AS film_likes
FROM film AS f
INNER JOIN like AS l ON f.id = l.film_id
GROUP BY f.name
ORDER BY COUNT(l.id) DESC
LIMIT 10
```

> Вывести друзей пользователя с id = 123

```sql
SELECT
  u.name
FROM user AS u
WHERE user.id IN (
    SELECT fs.friend_id
    FROM friendship AS fs
    WHERE user_id = 123
)
```

> Вывести общих друзей пользователя с id = 123 и id = 321

```sql
SELECT
  u.name
FROM user AS u
WHERE user.id IN (
    SELECT fs.friend_id
    FROM friendship AS fs
    WHERE fs.user_id = 123 and fs.friend_id in (
        SELECT fs1.friend_id
        FROM friendship AS fs1
        WHERE fs1.user_id = 321
    )
)
```
