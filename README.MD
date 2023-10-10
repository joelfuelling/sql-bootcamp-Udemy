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

### NOTE: We'll use <span style="color: yellow">yellow text</span> to note when we are using a PostGreSQL specific command.

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

### NOTE: <span style="color: lightgreen">You can sort by columns you didn't include in your query request statement. SQL knows that those fields are still there and can access them for purposes outside those we've seen so far.</span>

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
