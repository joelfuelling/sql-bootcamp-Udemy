<h1>Complete SQL Boot Camp: Go from Zero0️⃣ to Hero🦸‍♂️!</h1>

Databases are systems that allow users to store and organize data, GREAT with large sets of data. They contain a wide variety of users with various technical skill-sets (sales, ops, engineer, etc.)
</br>
</br>

# From Spreadsheets to Databases

<p>The first step to becoming a database administrator is to learn how to use spreadsheets. </p>

- Spreadsheets are great for small data sets, or a one-time analysis.
- Reasonably sized data set can be used
- Ability for untrained people to work with data.

</br>
Then we can move on to databases once we understand the spreadsheet.
</br>
</br>

- Better data integrity
- Can handle massive amounts of data
- Quickly combine different datasets
- Automate steps for ure
- Can support data for websites and applications

</br>
Databases have columns and rows just like a spreadsheet, but rather than a 'tab', we have individual 'tables' that contain a given dataset.</br>
</br>
</br>
For this tutorial we'll be using PostgreSQL, but keep in mind there are many other approaches and abstractions to working in SQL...

- MySQL, Oracle Databases, Microsoft Access, Amazon's Redshift, MemSQL, Periscope DAta, Hive (runs on top of hadoop), Google's BigQuery, Facebook's Presto.

</br>

<span style="font-size: 18px">NOTE:</span> <span style="color: lightgreen">We'll use <span style="color: yellow">yellow text</span> to note when we are using a PostGreSQL specific command.</span>

<br />
<br />

# SQL Syntax (can all be applied to any SQL database)

We use all caps for the SQL commands (though we could do lowercase) to differentiate them from the column, rows, or data objects we're accessing.

<br />
In general, it is not good practice to use an asterisk(*) in the SELECT statement if you don't really need all columns. It will automatically query everything, which increases traffic between the database server and the application, which can slow down the retrieval of results.

<br />

![Alt text](image.png)

<br />
<br />
<br />

The DISTINCT keyword operates on a column and returns only the distinct values in a column. The syntax is...
<br/>
<br/>

```
SELECT DISTINCT column_name FROM table_name
```

<br />
Or, you can place the column name in parenthesis
<br />
<br />

```
SELECT DISTINCT(column_name) FROM table_name
```

<br />
What if we have two of the same distinct instance within a column? We don't know if the returned data is the person with the name "David" as a duplicate entry, or two different people with the same first name... We only that David is one of the distinct 'first_name' values within that column.

### Other useful cases for DISTINCT.

<br />

1. How many different release years do we have? One, 2006 (results from query shown below).

```
SELECT DISTINCT release_year FROM film
```

<br />

2. How many different rental_rates are there? Three,

```
SELECT DISTINCT (rental_rate) FROM film
```

<br />
Let's say we have a visitor from Australia who't not familiar with our movie ratings system in the USA. We want to know... <br /> <br />

1. What types (or, distinct values) of ratings do we have in the database?
   "PG"
   "R"
   "NC-17"
   "PG-13" and
   "G"

```
SELECT DISTINCT rating FROM film;
```

<br />
<br />
<br />

# Count function

By default the count function returns the number of input rows of a table.

```
SELECT COUNT(*) FROM table_name
```

<br /><br />
By including a argument, the returned query will then match that specific argument/condition.

```
SELECT COUNT(first_name) FROM table_name
```

It will not work without () to pass in the value to be counted.
<br/><br/><br/>

# Comparison operators

- = equal to
- <> not equal to (or !=)
- '> greater than'
- < less than
- '> = greater than or equal to'
- <= less than or equal to

Along with comparison operators, there are 3 logical operators.
<br/><br/><br/>

## AND, OR, and NOT.

- AND - returns true if both conditions are true
- OR - returns true if either condition is true
- NOT - returns true if the condition is false
  <br/><br/>

```
SELECT first_name, choice FROM table_name
WHERE name = 'David'
AND choice = 'red'
```

<br />
How would we find the number of films with a rating or R or PG-13?
<br/>
<br/>

```
SELECT COUNT(*) FROM film
WHERE rating = 'R'
OR rating = 'PG-13'
```

<br/>
<br/>

# Where statement

One of the most fundamental statements alongside SELECT. With Where, we can specify conditions on columns for which rows to be returned. We decide what columns we want back, then the table, then WHERE to describe the conditions.
<br/>
<br/>

You can combine these in any fashion as long as spelling and syntax are correct. For example, we want the phone # from the customer with the address of '259 Ipoh Drive...

```
SELECT customer FROM customer
WHERE address = '259 Ipoh Drive'
```

<br />
<br />

# Order By

With Order By, we can sort the data by a column in either ascending or descending (order for strings, numerical for numbers)

Basic syntax for ORDER BY...

- Use ASC for ascending order _(Default if left blank)_
- Use DESC for descending order

```
SELECT column_1, column_2 FROM table_name
ORDER BY column_1 ASC/DESC
```

<br />
<br />
You can use ORDER BY on multiple columns. This makes a lot of sense with duplicate entries For example...
<br />
<br />

| Company | Name   | Sales |
| ------- | ------ | ----- |
| Apple   | Andrew | 100   |
| Google  | David  | 500   |
| Apple   | Zach   | 300   |
| Google  | Claire | 200   |
| Xerox   | Steven | 100   |

<br />
To sort by company and then sales in descending order:

```
SELECT company, sales FROM table
ORDER BY company, sales
```

<br />

| Company | Name   | Sales |
| ------- | ------ | ----- |
| Apple   | Andrew | 100   |
| Apple   | Zach   | 300   |
| Google  | Claire | 200   |
| Google  | David  | 500   |
| Xerox   | Steven | 100   |

<BR />

<span style="font-size: 18px">NOTE:</span> <span style="color: lightgreen">You can sort by columns you didn't include in your query request statement. SQL knows that those fields are still there and can access them for purposes outside those we've seen so far.</span>

<br />
<br />

# Limit

- The limit keyword allows us to limit the number of rows returned for a query.
- Useful for not wanting to return every single row in a table, but only view the top few rows to get an idea of the table layout.
- LIMIT also becomes useful in combination with ORDER BY.
- Goes at the very end of a query and is the last command to be executed.

### Limit Syntax:

```
SELECT * FROM payment
WHERE amount != 0.00
ORDER BY payment_date DESC
LIMIT(5)
```

This will return 5 recent payments (not 0) ordered by the payment date in descending order.
<br/>
<br/>
<br/>

# <span style="color: orange">POP QUIZ:</span>

<br />

<span style="color: orange">
1.</span>
 We want to reward the first 10 customers who made a payment. Write a query to gather the customer_ids.
<br />

```
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10
```

<br />

<span style="color: orange">
2.
</span> A customer wants to quickly rent a video over their short lunch break. What are the titles of the 5 shortest (length of runtime) movies?

```
SELECT title FROM film
ORDER BY length ASC
limit 5
```

Now that we know the shortest runtime ('length') is 46 minutes, we can query for how many films there are with that runtime instead of just returning 5. Coincidentally, there are 5 in this example for both queries.

```
SELECT title FROM film
WHERE length = '46'
```

<br />
<span style="font-size: 18px">NOTE:</span> 
<span style="color: lightgreen">'length' is actually a SQL keyword (which is why it's highlighted in PgAdmin), so be careful where you call it as a column name. Do your best to avoid column names that are the same as SQL keywords..</span>
<br />
<br />

<span style="color: orange">
BONUS:
</span>
If the previous customer can watch any movie that is 50 minutes or less in run time, how many options does she have? Answer: 37.

```
SELECT COUNT(title) FROM film
WHERE length <= '50'
```

<br />
<br />

# Between

Can be used to match a value against a range of values

- Value BETWEEN low AND high.
- (Value >= low) AND (value <= high).
- We include the low and high...

Combining NOT with BETWEEN...

- value NOT BETWEEN low and HIGH.
- (value < low) OR (value > high)
- We DO NOT include the low and high, only the value in between them.

<br/>
<br/>

## BETWEEN with DATES!

We can also use this on dates using the following syntax:

```
date_column BETWEEN start_date AND end_date
```

OR...

```
date BETWEEN '2007-01-01' AND '2007-02-01'
```

<span style="font-size: 18px">NOTE:</span>

1. <span style="color: lightgreen">You need to format dates in the ISO 8601 standard format, which is YYYY-MM-DD.</span>
2. <span style="color: lightgreen">When using BETWEEN operator with dates that also include timestamp information, pay careful attention to using BETWEEN versus <=, >= comparison operators, due to the fact that a datetime start with <span style="color: red">0:00.</span>

<br />
How many payments are there above, or below 9 dollars? <br />Answer: 14157

```
SELECT count(*) from payment
WHERE amount NOT BETWEEN 8 and 9
```

How many payments were there between February 1st, 2007, and February 15th, 2007?

```
SELECT * FROM payment
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15'
```

Remember Note 2. above? Here we have an example of this. We're only returning payments up to 2007-02-15, but not including them. We may want to include payments from the 15th, in which case we would search BETWEEN '2007-02-01' and '2007-02-16'

<br /><br />

# ~ IN ~

- You may want to check for multiple possible value options, for example, ir a user's name shows up IN/NOT IN list of options.
- We can use the IN/NOT IN operator to create a condition that checks to see if a value is included in a list of multiple options.

Syntax:

- ```
  value IN (option1, option2,...,option_n)
  ```
- ```
  WHERE color IN ('red', 'blue')
  ```
  <span style="color: lightGreen">NOT IN example:</span>
- ```
  WHERE color NOT IN ('green', 'blue')
  ```

Let's say we want to know the number of payments that are not '0.99', '1.98', or '1.99'.

```
SELECT * from payment
WHERE amount NOT IN (0.99, 1.98, 1.99)
ORDER BY amount ASC
```

<br />
<br />

# LIKE and ILIKE

What if we want to match against a general pattern in a string?

- All emails ending in '@gmail.com'.
- All names that begin with an 'A'.

The LIKE operator allows us to perform pattern matching against string data with the use of <span style="color: #ff6941">wildcard</span> characters:

- <span style="color: #ff6941; font-size: 24px">Percent %</span>
  - Matches any sequence of characters
- <span style="color: #ff6941; font-size: 24px">Underscore \_</span>
  - Matches any single character.

<br />

## Using %

- All names that <span style="color: orange">begin</span> with an 'A'.
  - WHERE name LIKE <span style="color: orange">'A%'</span>
  - Saying: match any name where the first letter is 'A' followed by and sequence of characters.
- All names that <span style="color: orange">end</span> with an 'a'
  - WHERE name LIKE <span style="color: orange">'%a'</span>
  - Saying: match any name where the last letter is 'a', preceded by and sequence of characters.

<br />

You can use ANY combinations of \_ and %! Let's find the first_name and email of anyone who has an 'er' in their name - How? Br wrapping % on both sides of what we're looking for we're asking for "any 'er' with any other chracters on either side".

```
SELECT first_name, email from customer
WHERE first_name ILIKE '%er%'
```

<br />

NOTE:

- <span style="color: lightGreen"> LIKE is case-sensitive, </span>
- <span style="color: lightGreen"> <span style="color: red">I</span>LIKE is case-<span style="color: red">in</span>sensitive, </span>

<br />
 
## Using \_

Using the underscore allows us to replace just a single character.

<br />

NOTE:

- <span style="color: lightGreen">You can combine LIKE and ILIKE operators for far greater detail
- <span style="color: lightGreen"><span style="background: darkred">REGEX expressions are fully supported in SQL!</span>

Get all customer that are some letter, followed by 'her', then any combination of letter.

```
SELECT first_name FROM customer
WHERE first_name LIKE '_her%'
```

How many peoples name starts with just the letter J?

```
SELECT count(*) FROM customer
WHERE first_name LIKE 'J%'
```

<br />
<br />
<br />

# <span style="color: purple; font-style: italic">CHALLENGE! 😰</span>

1. How many payment transactions were greater than $5.00?
   - ```
      SELECT COUNT(*) FROM payment
      WHERE amount > 5.00
     ```
2. How many actors have a first name that starts with a letter P?
   - ```
      SELECT COUNT(actor) FROM actor
      WHERE first_name LIKE 'P%'
     ```
3. How many unique districts are our customers from?
   - ```
     SELECT DISTINCT (COUNT(district)) from address
     ```
4. Retrieve the list of names for those distinct districts from the previous question.
   - ```
     SELECT DISTINCT (district) from address
     ```
5. How many films have a rating of R and a replacement cost between $5 and $15? Answer: 52.
   - ```
     SELECT COUNT(FILM) FROM film
     WHERE rating = 'R'
     AND replacement_cost BETWEEN 5 AND 15
     ```
6. How many films have the word Truman somewhere in the title?
   - ```
     SELECT COUNT(*) FROM film
     WHERE title LIKE '%Truman%'
     ```
