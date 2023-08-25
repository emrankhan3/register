## PostGreSql

#### ⚙ Installation ⚙

    1. Download PostGreSql
    2. Download PgAdmin
    3. install both
    4. restart your pc

### Fundamental

Q. How many payment transactions were greater than $5.00?

    SELECT COUNT(amount) FROM payment
    WHERE amount > 5;

Q. How many employee have a first name that starts with the letter P?

    SELECT COUNT(*) FROM emp
    WHERE first_name LIKE 'P%';

Q. How many unique districts are our customers from?

    SELECT COUNT(DISTINCT(district)) FROM customers

Q. Retrieve the list of names for those distinct districts from the previous question

    SELECT DISTINCT(district) FROM customers

Q. How many employee have a salary of 10000 and a replacement cost between $5000 and $15000?

    SELECT COUNT(*) FROM employees
    WHERE salary = 10000
    AND replacement_cost BETWEEN 5000 AND 15000;

Q. How many employee have the word mman somewhere in the first name?

    SELECT COUNT(*) FROM employees
    WHERE first_name ilike ='%mman%'

### Group BY statements

Q. We have two staff members, with Staff Id 1 and 2. We watn to give give a bonus to the staff member that handled the most payments.

How may payments did each staff member handle and who gets the bonus?

    SELECT staff_id, COUNT(amount) FROM payment
    GROUP BY staff_id

Q. Corporate HQ is conducting a study on the relationship between replament cost and a movie MPAA rating(e.g. G, PG, R, etc...)

What is the average replacement cost per MPAA rating?

    SELECT rating, avg(replacement_cost) FROM film
    GROUP BY rating

Q. We are running a promotion to reward our top 5 customers with coupons.

What are the customer ids of the top 5 customers by total spend?

    SELECT customer_id, SUM(amount) FROM payment
    GROUP BY customer_id
    ORDER BY (SUM(amount))
    LIMIT 5

### HAVING statements

Q. Get the customers who had 40 or more transaction payments

    SELECT customer_id, COUNT(amount) FROM payment
    GROUP BY customer_id
    HAVING COUNT(amount)>=40

Q. What are the customer ids of customers who have spent more than $100 in payment transaction with staff_id member 2?

    SELECT customer_id,staff_id, SUM(amount) FROM payment
    WHERE staff_id=2
    GROUP BY customer_id,staff_id
    HAVING SUM(amount)>=100

Q. What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?

    SELECT first_name,last_name FROM customer
    WHERE first_name LIKE 'E%'
    AND address_id <500
    ORDER BY customer_id DESC
    LIMIT 1;

### JOIN
Q. Chittagong sales tax laws have changed and we need to alert our customers to this through email.

What are the emails of the customers who live in Chittagong?

    SELECT address.address_id,district,email FROM address
    JOIN customer
    ON address.address_id = customer.address_id
    WHERE district = 'Chittagong'

 
Q. A customer walks in and is a huge fan of the actor "Emran Khan" and wants to know which movies he is in?

Get a list of all the movies "Emran Khan" has been in.

    SELECT title,first_name, last_name from actor
    LEFT JOIN film_actor
    ON actor.actor_id = film_actor.actor_id
    JOIN film
    ON film_actor.film_id = film.film_id
    where first_name = 'Emran' and last_name ='Khan'
