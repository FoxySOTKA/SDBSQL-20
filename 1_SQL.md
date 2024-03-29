# Домашнее задание к занятию «SQL. Часть 1»

## Выполнил Савицкий Андрей

### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

#### Результат:
#####  Командная строка -
````sql
select distinct district
from address 
where district like 'K%a' and 
district not like '% %';
````

#####  Скриншот работы -
<img width="645" alt="rayony from k to" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/4d1ad4b9-7db7-4c81-92d2-1bc531cfeadf">


### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

#### Результат:
#####  Командная строка -
````sql
select payment_id, amount, cast(payment_date as DATE)
from payment
where amount > 10.00 and 
payment_date between '2005:06:15 00:00:00' and '2005:06:18 23:59:59';
````

#####  Скриншот работы -
<img width="380" alt="prokat films" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/3c7a7616-db6b-4f5b-bd3f-8e35f4fa9fcb">


### Задание 3

Получите последние пять аренд фильмов.

#### Результат:
#####  Командная строка -
````sql
select rental_id, rental_date, cast(rental_date as DATE)
from rental 
order by rental_date desc 
limit 5;
````

#####  Скриншот работы -
<img width="381" alt="rental films" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/cb5ed22c-d302-4c01-be8e-c91b2ae99727">


### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

#### Результат:
#####  Командная строка -
````sql
select lower(first_name), lower(last_name),
replace(lower(first_name), 'll', 'pp'), replace(lower(last_name), 'll', 'pp')
from customer
where first_name = 'Kelly' or first_name = 'Willie' and 
active = '1';
````

#####  Скриншот работы -
<img width="418" alt="active pocupately" src="https://github.com/FoxySOTKA/SDBSQL-20/assets/141597247/fa429381-3b3f-42f1-ad45-99f961461505">



