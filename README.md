\# Домашнее задание к занятию "`SQL. Часть 1`" - `Корнилов Андрей`


\---

\### Задание 1

`Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.`

select district

from address

where district like 'K%' 

and district like '%a'

and district not like '% %';

![sakila1](https://github.com/AndreyTest010/sdb-homeworks/blob/main/sakila1.jpg)


\---

\### Задание 2

`Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.`


SELECT \*

FROM payment

WHERE payment\_date BETWEEN '2005-06-15' AND '2005-06-18 23:59:59'

AND amount > 10.00

ORDER BY payment\_date;

[sakila2](https://github.com/AndreyTest010/sdb-homeworks/blob/main/sakila2.jpg)


\---

\### Задание 3

`Получите последние пять аренд фильмов.`



SELECT \*

FROM rental

ORDER BY rental\_date DESC

LIMIT 5;



![sakila3](https://github.com/AndreyTest010/sdb-homeworks/blob/main/sakila3.jpg)

\### Задание 4

`Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,

замените буквы 'll' в именах на 'pp'.`



SELECT replace(lower(first\_name), 'll', 'pp') AS first\_name,

(LOWER(last\_name)) AS last\_name

FROM customer

WHERE (first\_name = 'Kelly' OR first\_name = 'Willie')

AND active = 1;



![sakila4](https://github.com/AndreyTest010/sdb-homeworks/blob/main/sakila4.jpg)

\### Задание 5

`Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.`


SELECT

LEFT(email, LOCATE('@', email) - 1) AS email\_do,

SUBSTRING\_INDEX(email, '@', -1) AS email\_posle

FROM customer;



![sakila5](https://github.com/AndreyTest010/sdb-homeworks/blob/main/sakila5.jpg)


\### Задание 6

`Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.`



SELECT

CONCAT(UPPER(LEFT(SUBSTRING\_INDEX(email, '@', 1), 1)), LOWER(SUBSTRING(SUBSTRING\_INDEX(email, '@', 1), 2))) AS email\_do,

CONCAT(UPPER(LEFT(SUBSTRING\_INDEX(email, '@', -1), 1)), LOWER(SUBSTRING(SUBSTRING\_INDEX(email, '@', -1), 2))) AS email\_posle

FROM customer;


![sakila6](https://github.com/AndreyTest010/sdb-homeworks/blob/main/sakila6.jpg)
