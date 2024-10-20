# Домашнее задание к занятию "SQL. Часть 2" - `Lebedev Boris`

# Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.

```SELECT concat(sf.first_name , ' ', sf.last_name) AS 'Full Name', cy.city, COUNT(cr.customer_id) AS 'Count Consumers'        
FROM sakila.store s
INNER JOIN sakila.staff sf on sf.store_id = s.store_id
INNER JOIN sakila.customer cr on cr.store_id = s.store_id
INNER JOIN sakila.address a on a.address_id = s.address_id
INNER JOIN sakila.city cy on cy.city_id = a.city_id
GROUP BY sf.staff_id, cy.city_id
HAVING COUNT(cr.customer_id) > 300;
```


![alt text](https://github.com/bris91/12-04/blob/437abfb6be832c7df463c2dd81fdff3b9d9e59e5/1.png)




# Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```SELECT COUNT(f.title)
FROM sakila.film f  
WHERE f.`length` > (SELECT AVG(`length`) FROM sakila.film);
```

![alt text](https://github.com/bris91/12-04/blob/437abfb6be832c7df463c2dd81fdff3b9d9e59e5/2.png)


# Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```SELECT SUM(amount) Платеж, DATE_FORMAT(payment_date, '%Y-%m') Месяц, COUNT(rental_id) Количество_аренд
FROM sakila.payment
GROUP BY DATE_FORMAT(payment_date, '%Y-%m')
ORDER BY SUM(amount) DESC
LIMIT 1;
```

![alt text](https://github.com/bris91/12-04/blob/437abfb6be832c7df463c2dd81fdff3b9d9e59e5/3.png)
