# POSTGRESQL DATABASE NOTES

## What is a database?

A database is a place that you can store, manipulate and retrive data.

## listing all the available databases

> > > \l

## Connection Options

-h -> hostname,
-p -> password,
-U -> username,
-w -> no password,
-W -> password

## Connecting to a database via the terminal

> > > psql -h localhost -p 5432 -U postgres tests

OR

> > > \c database_name

## DATA TYPES

PostgreSQL offers a variety of data types to handle different kinds of data. The most commonly used PostgreSQL data types include:

Numeric Types:

1. integer: A 32-bit signed integer.
2. bigint: A 64-bit signed integer.
3. decimal or numeric: Fixed-point numbers.
4. real: Single-precision floating-point numbers.
5. double precision: Double-precision floating-point numbers.

Character Types:

1. character(n): Fixed-length character strings.
2. varchar(n): Variable-length character strings.
3. text: Variable-length character strings (no specified length).

Date/Time Types:

1. date: Calendar date (year, month, day).
2. time: Time of day.
3. timestamp: Date and time.

Boolean Type:

1. boolean: True or false values.

Array Types:

1. Arrays of any data type, denoted by appending [] to the base type (e.g., integer[]).

JSON Types:

1. json: Stores JSON-formatted data.
2. jsonb: Binary representation of JSON, more efficient for certain operations.

Geometric Types:

1. point: Represents a point in a 2D plane.
2. line: Represents an infinite line in a 2D plane.
3. circle: Represents a circle in a 2D plane.

Network Address Types:

1. inet: IPv4 or IPv6 host address.
2. cidr: IPv4 or IPv6 network address.

Bit String Types:

1. bit(n): Fixed-length bit string.
2. bit varying(n): Variable-length bit string.

UUID Type:

1. uuid: Universally unique identifier.

Enumerated Types:

1. enum: User-defined enumerated types.

Hstore Type:

1. hstore: Stores sets of key/value pairs.

## HOW TO MAKE A DATABASE READONLY

> > > ALTER DATABASE MyDB READ ONLY = 1;

## HOW TO DISABLE READONLY MODE

> > > ALTER DATABASE MyDB READ ONLY = 0;

## SQL DATA MANIPULATION COMMANDS

Command, Option or Operator:

1. SELECT
2. WHERE
3. GROUP BY
4. HAVING
5. ORDER BY
6. INSERT
7. UPDATE
8. DELETE

Logical Operators:

1. AND
2. OR
3. NOT

Special Operators:

1. BETWEEN
2. IN
3. LIKE
4. IS NULL
5. EXITS
6. DISTINCT

Aggregate Functions:

1. COUNT
2. MIN
3. MAX
4. SUM
5. AVG

## How to create a table

CREATE TABLE table_name(
column_name data type constraints if any
);

CREATE TABLE person(
id INT,
first_name VARCHAR(50),
last_name VARCHAR(50),
gender VARCHAR(6),
date_of_birth TIMESTAMP,
);

## How to show the tables in the database

> > > \d

Showing a specific table description

> > > \d table_name

## Creating a table with constraints

CREATE TABLE person(
id BIGSERIAL NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50) NOT NULL,
gender VARCHAR(7) NOT NULL,
date_of_birth DATE NOT NULL,
);

## Adding a Column to a table

> > > ALTER TABLE person ADD email VARCHAR(150);

## HOW TO SELECT A TABLE

> > > SELECT \* FROM employees;

## HOW TO RENAME A TABLE

> > > RENAME TABLE orginal_name TO new_name;

## TO DELETE/DROP A TABLE

> > > DROP TABLE table_name;

## ALTER A TABLE

> > > ALTER TABLE employees
> > > ADD phone_number VARCHAR(15);

## RENAMING A COLUMN IN A TABLE

> > > ALTER TABLE employees
> > > RENAME COLUMN phone_name TO email;

## CHANGING THE DATATYPE OF A COLUMN

> > > ALTER TABLE employees
> > > MODIFY COLUMN email VARCHAR(150);

## HOW TO MOVE COLUMNS AROUND AND CHANGE THERE POSITIONS IN THE TABLE

> > > ALTER TABLE employees
> > > MODIFY email VARCHAR(150)
> > > AFTER last_name;

## DROP/DELETE A COLUMN FROM A TABLE

> > > ALTER TABLE employees
> > > DROP COLUMN email;

## HOW TO INSERT DATA OR ROWS IN A TABLE

> > > INSERT INTO person(first_name, last_name, gender, date_of_birth) VALUES ("Anna", "Smith", DATE "1988-01-09->(year-month-day));

> > > INSERT INTO employees
> > > VALUES(1, "Eugene", "Krabs", 25.50, "2023-01-02");

## INSERTING MULTIPLE ROWS AT ONCE

> > > INSERT INTO employees
> > > VALUES(2, "Squidward", "Tentacles", 15:00, "2023-01-03"),
> > > (3, "Spongebob", "Squarepants", 12.50, "2023-01-04"),
> > > (4, "Patrick", "Star", 12:50, "2023-01-05"),
> > > (5, "Sandy", "Cheeks", 17:25, "2023-01-06");

## INSERTING DATA TO ONLY PARTS OF THE ROW

> > > INSERT INTO employees(employee_id, first_name, last_name)
> > > VALUES(6, "Sheldon", "Plankton");

## SELECTING DATA FROM A TABLE

> > > SELECT \* FROM employees;

> > > SECECT first_name, last_name FROM employees;

> > > SELECT \* FROM employees WHERE employee_id = 1;

> > > SELECT \* FROM employees WHERE first_name = "Spongebob" ;

> > > SELECT \* FROM empoyees WHERE hourly_pay > 12.50;

> > > SELECT \* FROM employees WHERE hourly_pay != 12.50;

> > > SELECT \* FROM person WHERE country = 'Kenya';

> > > SELECT \* FROM persom WHERE gender = 'Female';

> > > SELECT \* FROM person WHERE gender = "Male" AND country = "Poland";

> > > SELECT \* FORM person WHERE gender = 'Female' AND (country = 'Poland OR country = 'China');

> > > SELECT \* FORM person WHERE gender = 'Female' AND (country = 'Poland OR country = 'China') AND first_name = 'jane';

> > > SELECT \* FROM person WHERE country IN ('China', 'France', 'Brazil','Mexico');

> > > SELECT \* FROM person WHERE country IN ('China', 'France', 'Brazil','Mexico') ORDER BY country;

> > > SELECT \* FROM person WHERE date_of_birth BETWEEN '2000-01-01' AND '2010-01-01';

## Selecting all the emails that end with .com

> > > SELECT \* FROM person WHERE email LIKE '%.com';

> > > SELECT \* FROM person WHERE email LIKE '%@bloomberg.com';

> > > SELECT \* FROM person WHERE email LIKE '%@gmail.com';

> > > SELECT \* FROM person WHERE email LIKE '%@google.%';

> > > SELECT \* FROM person WHERE email LIKE '**\_\_\_\_**@%';

> > > SELECT email, COUNT(\*) FROM person GROUP BY email HAVING COUNT(\*) > 1;

## Limiting the number of records you get back

> > > SELECT \* FROM person LIMIT 10;

> > > SELECT \* FROM person OFFSET 5 LIMIT 5; starts from 5 to 10

> > > SELECT \* FROM person OFFSET 5 FETCH FIRST 15 ROW ONLY;

## Ordering data in asending or desending order

> > > SELECT \* FROM person ORDER BY email;

> > > SELECT \* first_name FROM person ORDER BY first_name;

> > > SELECT \* first_name FROM person ORDER BY first_name DESC;

## getting the only the unique data from a column in a table

> > > SELECT DISTINCT country FROM person ORDER BY country;

## Grouping data by a column

> > > SELECT country, COUNT(\*) FROM person GROUP BY country;

> > > SELECT country, COUNT(\*) FROM person GROUP BY country ORDER BY country;

## Finding the group that has more than five people

> > > SELECT country, COUNT(\*) FROM person GROUP BY country HAVING COUNT(\*) > 5;

> > > SELECT country, COUNT(\*) FROM person GROUP BY country HAVING COUNT(\*) > 5 ORDER BY country;

## Finding the maximum number

> > > SELECT MAX(price) FROM car;

## Finding the minimum number

> > > SELECT MIN(price) FROM car;

## Finding the average price of the cars

> > > SELECT AVG(price) FROM car;

## ROUNDING NUMBERS

> > > SELECT ROUND(AVG(price)) FROM car;

## GETING THE AVERAGE PRICE OF EACH MAKE OF CAR

> > > SELECT make, model, MIN(price) FROM car GROUP BY make, model;

## Performing Addition with our data set

> > > SELECT SUM(price) FROM car;

> > > SELECT make, model, SUM(price) FROM car GROUP BY make, model;

## Promotional Price

> > > SELECT id, make , model, price, price \* 0.1 FROM car;

> > > SELECT id, make , model, price, ROUND(price \* 0.1, 2) FROM car;

> > > SELECT id, make , model, price AS original_price, ROUND(price \* 0.1, 2) AS discount, (price - ROUND(price \* 0.1,2)) AS price_after_discount FROM car;

## Selecting all the emails from the databse and if someone doesn have one we say email not provided

> > > SELECT COALESCE(email, "Email Not Provided") FROM person;

## Dates In Postgresl

1. Getting the actual date and time: SELECT NOW()
2. Getting the date: SELECT NOW()::DATE;
3. Getting the time: SELECT NOW()::TIME;

## Adding and substracting dates

1. SELECT NOW() - INTERVAL '10 YEARS';
2. SELECT NOW() - INTERVAL '10 MONTHS';
3. SELECT NOW() - INTERVAL '10 DAYS';

## Calculating Peoples Age

> > > SELECT first_name, last_name, gender, country, date_of_birth, AGE(NOW(), date_of_birth) AS age FROM person;

## PRIMARY KEYS

Primary Keys are unique columns in a table that are used to identify a person to thing.
Primary Keys are unique to each item, therefore two rows cant have the same primary key.

## Droping Constraints from a table

> > > ALTER TABLE person DROP CONSTRAINT person_pkey;

## Adding a primary key

> > > ALTER TABLE person ADD PRIMARY KEY (id)
