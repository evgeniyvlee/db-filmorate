# db-filmorate
DB scheme for filmorate app

> Вывести 10 популярных фильмов

```sql
SELECT f.id, f.name, f.description, f.releasedate, f.duration, f.mpa_id, m.name AS mpa_name, COUNT(f.id)
FROM films f
JOIN mpa m ON f.mpa_id = m.id
LEFT JOIN film_like AS fl ON f.id = fl.film_id
GROUP BY f.name
ORDER BY COUNT(f.id) DESC, f.id DESC
LIMIT 10;
```

> Вывести друзей пользователя с id = 123

```sql
SELECT id, name, login, email, birthday
FROM users WHERE users.id IN (SELECT friend_id FROM friendship WHERE user_id = 123);
```

> Вывести общих друзей пользователя с id = 123 и id = 321

```sql
SELECT u.id, u.name, u.login, u.email, u.birthday
FROM users u
WHERE u.id IN (
  SELECT f.friend_id
  FROM friendship f, friendship f2
  WHERE f.user_id = 123 AND f2.user_id = 321 AND f.friend_id = f2.friend_id
);
```
