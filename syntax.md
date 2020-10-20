

# POSTGRES terminal commands

1. way to connect to DB => psql -h localhost -p 5432 -U <yourUserName> <db_name>
2. way to connect to DB => run psql from terminal then run \c <db_name> 

- \? - all info
- \l - list of databases
- \dt - show tables
- \d table_name - more detailed table info
- \x - expanded display is on

```
CREATE DATABASE db_name;
DROP DATABASE db_name; => be careful
CREATE TABLE tb_name;
DROP TABLE tb_name; => be careful
INSERT INTO tb_name (values, ...) VALUES (values, ...)
SELECT * FROM tb_name;
```

=> More random examples: 

```
SELECT * FROM tb_name ORDER BY <column_name> ASC;

SELECT * FROM tb_name ORDER BY <column_name> DESC;
<!-- When sorting only use at most 1 column  -->

SELECT <column_name> FROM tb_name;

SELECT DISTINCT <column_name> FROM tb_name; -> unique values/remove duplicates

SELECT * FROM tb_name WHERE <city> = 'Bishkek';

SELECT * FROM tb_name WHERE <city> = 'Bishkek' AND (country = 'Kyrgyzstan' OR country = 'Kyrgyz Republic');

SELECT <column_name> FROM tb_name LIMIT 10; -> limit result to 10(or any number)

SELECT <column_name> FROM tb_name OFFSET 5 LIMIT 10; -> starting from 10 give 5 results

SELECT <column_name> FROM tb_name OFFSET 5; -> start from line 5

SELECT * FROM tb_name WHERE <city> IN ('Bishkek', 'Paris', 'London'); -> equals to SELECT * FROM tb_name WHERE <city> = 'Bishkek' OR <city> = 'Paris' OR <city> = 'London';

SELECT * FROM tb_name WHERE <city> = 'Bishkek';

SELECT * FROM tb_name WHERE <age> BETWEEN '2001-01-01' AND '2020-02-02';

SELECT * FROM tb_name WHERE <email> LIKE '%bloomberg.%'; -> anyone with bloomberg email

SELECT * FROM tb_name WHERE <email> LIKE '___'; -> anyone with bloomberg email

SELECT * FROM tb_name WHERE <country> LIKE 'P%'; -> anyone that starts P

SELECT * FROM tb_name WHERE <country> ILIKE 'P%'; -> anyone that starts P or p. Ignores the case


SELECT <country_of_birth>, COUNT(*) FROM tb_name GROUP BY <country_of_birth> ORDER BY <country_of_birth> -> statistics, aggregation and filtering
<!-- https://www.postgresql.org/docs/9.5/functions-aggregate.html -->

SELECT <country_of_birth>, COUNT(*) FROM tb_name GROUP BY <country_of_birth> HAVING COUNT(*) > 5 ORDER BY <country_of_birth> -> statistics, aggregation and filtering. HAVING used with GROUP BY and should come before ORDER BY
``` 


## arithmetic operations
```
SELECT MAX(<price>) FROM tb_name;

SELECT MIN(<price>) FROM tb_name;

SELECT AVG(<price>) FROM tb_name;

SELECT ROUND(<price>) FROM tb_name;

SELECT make, model MIN(<price>) FROM tb_name GROUP BY make, model;

SELECT id, make, model, price, ROUND(price * .10, 2), ROUND(price - (price * .10), 2) FROM car; -> give 10% discount on car actual prices

SELECT id, make, model, price AS original_price, ROUND(price * .10, 2) AS ten_percent, ROUND(price - (price * .10), 2) AS discount_after_ten_percent FROM car; -> give 10% discount on car actual prices

SELECT COALESCE(email, 'Email not provided') FROM tb_name; -> fill NULL values

SELECT COALESCE(10 / NULLIF(0, 0), 0);

SELECT NOW(); -> current date

SELECT NOW() - INTERVAL '10 YEARS'; -> 10 years back

SELECT EXTRACT(YEAR FROM NOW);

ALTER TABLE tb_name ADD PRIMARY KEY (id); -> make sure id unique

ALTER TABLE tb_name ADD CONSTRAINT unique_email_address UNIQUE (email); -> make sure email unique
  : same as above just name is provided by Postgres -> ALTER TABLE tb_name ADD UNIQUE (email)

ALTER TABLE tb_name DROP CONSTRAINT unique_email_address UNIQUE (email); 

ALTER TABLE tb_name ADD CONSTRAINT gender_contstraint CHECK(gender == 'Female' OR gender = 'Male'); -> only allow Female and Male genders
```

## delete
```
DELETE * FROM tb_name; -> be careful

DELETE FROM tb_name WHERE id = 1;

DELETE FROM tb_name WHERE id = 1;
```

## update and more
```
UPDATE person SET email = "test@test.com" WHERE id = 1;

UPDATE person SET first_name = 'Neo', email = "test@test.com" WHERE id = 1;

ON CONFLICT (id) DO NOTHING; -> handle duplicate key, email etc. errors
```

## foreign keys and joins
## relationships between tables

```
UDPATE person SET car_id = 2 WHERE id = 1;
```

## inner joins
```
SELECT * FROM person
JOIN car ON person.car_id = car.id;

SELECT person.first_name, car.make FROM person
JOIN car ON person.car_id = car.id;
```

## left joins
```
SELECT * FROM person
LEFT JOIN car ON person.car_id = car.id;

SELECT * FROM person
LEFT JOIN car ON person.car_id = car.id
WHERE car.* IS NULL;
```
## export to csv
```
\copy(SELECT * FROM person LEFT JOIN car ON person.car_id = car.id) TO '/Users/ulan/Desktop/results.csv' DELIMETER ',' CSV HEADER;
```
#### we can also use functions etc...
#### for more check documentation or run \? 



















