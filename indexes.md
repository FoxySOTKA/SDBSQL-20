# Домашнее задание к занятию «Индексы»

## Выполнил Савицкий Андрей

### Задание 1

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

#### Запрос:
````
select (sum(INDEX_LENGTH)/sum(DATA_LENGTH))*100 as 'INDEXES'
from information_schema.TABLES t;
````

#### Результат:
<img width="473" alt="index" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/4ab1f856-d146-447b-bb50-f0a982791d50">


### Задание 2 с ответом и корректировкой

Выполните explain analyze следующего запроса:
````sql
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id
````
#### - перечислите узкие места:
После explain analyze запроса было получено, что наиболее узким местом в данном запросе является излишние обрабатывание таблицы оконной функцией. Так как нужно посчитать сумму платежей покупателей за конкретную дату, обработка и присоединение так***ой*** таблиц***ы*** как ~~inventory, rental и~~ film не имеет смысла, ведь ***её*** данные дальше не используются. Все необходимые данные уже есть в таблицах payment и customer, ***а таблицы inventory и rental задают опредленные продажи. Поэтому мы убираем film. 
- ***Так как мы убрали film оконная функция теряет свой смысл и её нужно переписать на group by и нужно создать соединение на cross join.*** 
- ***Второе узкое место - оптимальное использование mysql-ом индекса (ему мешает оператор date) -нужно переписать условие where для payment_date.***
#### - оптимизируйте запрос (внесите корректировки по использованию операторов, при необходимости добавьте индексы):
````sql
explain analyze
select concat(c.last_name, ' ', c.first_name) as customer_name, sum(pay.amount) 
from customer c
inner join payment pay on pay.customer_id = c.customer_id
inner join rental ren on ren.rental_id = pay.rental_id 
where payment_date >= '2005-07-30' and payment_date < date_add('2005-07-30', interval 1 day)
group by customer_name
````
#### - скрин работы explain analyze:
<img width="958" alt="исправление по индексам" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/8bca9629-0ea0-4e45-b582-75dd5b5c4775">


