# Домашнее задание к занятию «Работа с данными (DDL/DML)»

## Выполнил Савицкий Андрей

### Задание 1 сразу с ответами и скринами
1.1. Поднимаю чистый инстанс MySQL версии 8.0+: 

````
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'ol';
````

1.2. Создаю учётную запись sys_temp: 

````
SELECT host, user FROM mysql.user;
````

1.3. Выполняю запрос на получение списка пользователей в базе данных: 
<img width="547" alt="список в бд" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/a8cbec3c-1020-469b-9abd-d88fcc5aec43">


1.4. Даю все права для пользователя sys_temp: 
````
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';
````

1.5. Выполняю запрос на получение списка прав для пользователя sys_temp: 
<img width="566" alt="список пользователей в бд" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/4608bd3f-8649-49ad-ac24-ed39dd760f8c">

1.6. Переподключаюсь к базе данных от имени sys_temp:
````
mysql -u sys_temp -p
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'ol';
````

Для смены типа аутентификации с sha2 использую запрос: 
````
sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
````
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачиваю дамп базы данных.

1.7. Восстановливаю дамп в базу данных.

1.8. ER-диаграмма получившейся базы данных: (скриншот)

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```


