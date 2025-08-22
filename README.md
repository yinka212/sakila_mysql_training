# MYQSL PRACTICE USING SAKILA SCHEMA

## Table of Content
- [Overview](#overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Exercise](#exercise)
- [Reference](#references)
### Overview
This data analysis project is my first effort at using Github as my repository for data analytical work. 
This work contains 10 questions that is from beginner to some level of advancement.I hope you find the review worth your time.

### Data Source
The database used is sakila schema obtainable from mysql website.
[Download here](https://downloads.mysql.com/docs/world-db.zip)

### Tools 
- Mysql workbench

### Exercise 

#### 10  Sample Queries for Data Analytics using SAKILA Database
```mysql
 1) All films WITH PG-13 films WITH rental rates of 2.99 or lower

SELECT f.film_id,f.title,f.description, f.release_year,f.rating,f.releASe_year FROM sakila.film f
WHERE f.rating='PG-13' AND f.rental_rate <=2.99;     

2) All documentary films that have deleted scenes
SELECT f.film_id, f.title, f.special_features,f.releASe_year FROM sakila.film f 
WHERE f.special_features LIKE ('%commentaries%' '%Deleted Scenes%');

 3)  A list of all inactive customers, 
SELECT c.customer_id, concat(first_name, '  ',  last_name) full_name, c.email FROM sakila.customer c
WHERE c.active=0;

4) How many are the inactive customers?
SELECT count(c.active) NON_Active FROM Sakila.customer c
WHERE c.active=0;

5) Names of Customers who rented a movie ON 26th July, 2005
SELECT r.customer_id, concat(c.first_name, '   ',c.last_name)full_name, c.email FROM sakila.rental r
JOIN sakila.customer c ON r.customer_id=c.customer_id
WHERE DATE (r.rental_date)= '2005-07-26';
SELECT count(rental_date)no_bought FROM sakila.rental
WHERE DATE(rental.rental_date) ='2005-07-26';

6) Distinct names of Customers who rented a movie of 26th July 2005
SELECT DISTINCT concat(first_name, '   ', last_name) full_name FROM sakila.rental r
 JOIN sakila.customer c ON r.customer_id=c.customer_id
WHERE DATE (r.rental_date)= '2005-07-26';

7) How many rentals were done on each week and mONth 
SELECT MONTH (rental_date) month_of_the_year, week(rental_date) week_of_the_year, sum(amount) FROM sakila.rental
JOIN sakila.payment
ON sakila.rental.customer_id= sakila.payment.customer_id
WHERE rental_date >='2005-05-01'AND rental_date <= '2005-08-31'
 GROUP BY MONTH ( rental_date), WEEK(rental_date) WITH rollup;

8) All children films in the catalogue
SELECT * FROM sakila.category; #this line reveals the place WHERE we identify the children film and the code
SELECT * FROM Sakila.film_category fc WHERE category_id=3;
(we then combine the 3 tables using the JOIN command )
SELECT fc.film_id,f.title,f.releASe_year,f.rating FROM sakila.film_category fc 
JOIN sakila.category c  ON fc.category_id= c.category_id
JOIN sakila.film f ON fc.film_id= f.film_id
WHERE sakila.c.name= 'children';

9) customers and how many movies were rented so far
SELECT r.rental_id,r.customer_id FROM sakila.rental r;
SELECT r.customer_id, concat(c.first_name,  '  ',c.last_name )full_name,email, count(*) count  FROM sakila.rental r
JOIN sakila.customer c ON r.customer_id=c.customer_id
GROUP BY r.customer_id;

10) Which movies whould be discONtinued due to low patrONage (less than 1 lifetimes) using commON terminal expressiONs
 WITH low_patronage AS 
	(SELECT r.inventory_id, count(*) count FROM sakila.rental r
	GROUP BY r.inventory_id
	HAVING count<=1)
SELECT low_patronage.inventory_id,i.film_id,f.title
FROM low_patronage
JOIN sakila.inventory i ON low_patrONage.inventory_id= i.inventory_id
JOIN sakila.film f ON i.film_id=f.film_id;

```
### References
I receive great assistance from youtube and w3resources 

i just typed this as a addendum to say thank you for checking this out 
  
