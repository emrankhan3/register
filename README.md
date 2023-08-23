
## PostGreSql
#### ⚙  Installation ⚙
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

