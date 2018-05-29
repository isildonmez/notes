> From [Odin Project's curriculum](https://www.theodinproject.com/courses/databases/lessons/databases)

### Introduction

We’ve talked about the client-side and the server-side but how do we keep ahold of all our user’s data? Who remembers that your login password is CatLover1985 so you can sign into the website? The bottom layer of any web application is the database and it handles all the remembering for you (we’ll cover caching much later). It can be relatively simple, like an excel spreadsheet, or incredibly complex and split into many giant pieces like Facebook’s.

Compared to a normal programming language like you’ve already learned, SQL (Structured Query Language), which is used to query databases, is a very simple syntax… there are only a small handful of verbs to learn. What trips people up is that you need to be able to visualize in your head what it’s going to be doing.

> From [Odin Project's curriculum](https://www.theodinproject.com/courses/databases/lessons/databases-and-sql)

### The World’s Fastest Semi-Complete Explanation of SQL

#### Setting Stuff Up

The setup information for your database is stored in a special file called the “Schema”, and this is updated whenever you make changes to the structure of your database. Think of the schema as saying “here’s our database and it’s got a couple tables. The first table is ‘users’ and it’s got columns for ‘ID’ (which is an integer), ‘name’ (which is a bunch of characters), ‘email’ (which is a bunch of characters) …”

In addition to setting up tables, you can tell your database to only allow unique values in a particular column (e.g. for usernames) or to index a column for faster searching later with `CREATE INDEX`. Create indexes, which basically do all the hard work of sorting your table ahead of time, for columns that you’ll likely be using to search on later (like username)… it will make your database much faster.

SQL likes semicolons at the end of lines and using single quotes (‘) instead of double quotes(“).

#### Mucking Around With Data

You can do all kinds of common sense things like using `>`, `<`, `<=` etc. comparison operators to specify groups of rows to run commands on or logical operators like `AND`, `OR`, `NOT` etc to chain multiple clauses together, e.g. `DELETE * FROM users WHERE id > 12 AND name = 'foo'`.

“Create” queries use `INSERT INTO` and you’ll need to specify which columns to insert stuff into and then which values to put in those columns, which looks something like `INSERT INTO Users (name, email) VALUES ('foobar','foo@bar.com');`.

“Update” queries use `UPDATE` and you’ll need to tell it what data to `SET` (using key=”value” pairs) and which rows to do those updates for. Be careful because if your `WHERE` clause finds multiple rows (e.g. if you’ve searched based on a common first name), they’ll all get updated.

```
UPDATE Users
SET name='barfoo', email='bar@foo.com'
WHERE email='foo@bar.com';
```

“Read” queries, which use `SELECT`, are the most common, e.g. `SELECT * FROM users WHERE created_at < '2013-12-11 15:35:59 -0800'`. If there are more than one table involved use `SELECT users.id, users.name FROM users`. If you want a list of all the different names of your users without any duplicates, try `SELECT DISTINCT users.name FROM users`.

#### Mashing Tables Together

- `INNER JOIN`, aka `JOIN`: `SELECT * FROM TableA INNER JOIN TableB ON TableA.name = TableB.name`

- `LEFT OUTER JOIN`: `SELECT * FROM TableA LEFT OUTER JOIN TableB ON TableA.name = TableB.name`. For A\B: `SELECT * FROM TableA LEFT OUTER JOIN TableB ON TableA.name = TableB.name WHERE TableB.id IS null`

- `RIGHT OUTER JOIN`: the opposite… keep all rows in the right table.

- `FULL OUTER JOIN`: `SELECT * FROM TableA FULL OUTER JOIN TableB ON TableA.name = TableB.name` (A || B). For ((A\B) || (B\A)): `SELECT * FROM TableA FULL OUTER JOIN TableB ON TableA.name = TableB.name WHERE TableA.id IS null OR TableB.id IS null`

#### Using Functions to Aggregate Your Data

Sometimes you want to just return a single relevant value that aggregates a column, like the `COUNT` of posts a user has written. In this case, just use one of the helpful “aggregate” functions offered by SQL (most of which you’d expect to be there – functions like `SUM` and `MIN` and `MAX` etc). You include the function as a part of the `SELECT` statement, like `SELECT MAX(users.age) FROM users`.

You often see aliases (`AS`) used to rename columns or aggregate functions so you can call them by that alias later, e.g. `SELECT MAX(users.age) AS highest_age FROM users` will return a column called `highest_age` with the maximum age in it.

Displaying the `COUNT` of posts for EACH user (as opposed to the count of all posts by all users:

```
SELECT users.name, COUNT(posts.*) AS posts_written
FROM users
JOIN posts ON users.id = posts.user_id
GROUP BY users.name;
```

If you’ve used an aggregate function like `COUNT` (say to get the count of posts written for each user in the example above), `WHERE` won’t work anymore. So to conditionally retrieve records based on aggregate functions, you use the `HAVING` function, which is essentially the `WHERE` for aggregates. So say I only want to display users who have written more than 10 posts:

```
SELECT users.name, COUNT(posts.*) AS posts_written
FROM users
JOIN posts ON users.id = posts.user_id
GROUP BY users.name
HAVING posts_written >= 10;
```

### SQL id faster than Ruby

For instance, if you want all the unique names of your users, you COULD just grab the whole list from your database using SQL like `SELECT users.name FROM users` (which Active Record will do for you with `User.select(:name)`) then remove duplicates using Ruby’s `#uniq` method, e.g. `User.select(:name).uniq`… but that requires you to pull all that data out of your database and then put it into memory and then iterate through it using Ruby. Use `SELECT DISTINCT users.name FROM users` instead to have SQL do it all in one step.















