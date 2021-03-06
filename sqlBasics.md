- Databases come in many forms: Spatial, Non-relational, Graph, XML... But a really popular type of database is called Relational Database.

- RD: stores each kind of data in a Table which is a kind of like storing data in a spreadsheet. makes it particularly easy to form relationships between tables. As an example, for Khan academy they might have a users table and a badges table; and a table includes only user id and badge id.

- Most databases come with a Query language to interact with the database. *SQL* is a language designed entirely for accessing databases, and is the most popular of them. With SQL, we can create tables, change data, get back to data that we're interested in.

```sql
CREATE TABLE meetups (id INTEGER PRIMARY KEY, name TEXT, day TEXT, time INTEGER);

INSERT INTO meetups VALUES(1, "Phoenetics", "monday", 3);
INSERT INTO meetups VALUES(2, "Conversation", "wednesday", 5);
INSERT INTO meetups VALUES(3, "Phoenetics", "tuesday", 3);
INSERT INTO meetups VALUES(4, "Socialization", "wednesday", 7);
INSERT INTO meetups VALUES(5, "Socialization", "friday", 5);

SELECT name FROM meetups; /*Only names*/
SELECT * FROM meetups; /*whole sheet*/
SELECT * FROM meetups ORDER BY name; /*ordered as names together*/
SELECT * FROM meetups ORDER BY day; /*ordered as names together*/
SELECT * FROM meetups WHERE time > 3 ORDER BY day; /* only the ones are later than 3*/
SELECT SUM(time) FROM meetups;
SELECT MAX(id) FROM meetups; /*the number of element in the data*/
SELECT day, SUM(time) FROM meetups GROUP BY day; /*days and their total times*/
```

#### Relational Databases vs Non Relational Databases

Relational databases like MySQL, PostgreSQL and SQLite3 represent and store data in tables and rows. They're based on a branch of algebraic set theory known as relational algebra. Relational databases use Structured Querying Language (SQL), making them a good choice for applications that involve the management of several transactions. It allows you to link to other tables.


Meanwhile, non-relational databases like MongoDB represent data in collections of JSON documents. The Mongo import utility can import JSON, CSV and TSV file formats. Mongo query targets of data are technically represented as BSON (binary JSON).

#### XML vs Relational Databases

XML is more flexible structure than a database table can offer. When you have data that you do not know exactly the structure beforehand, it could be profitable to store it as XML.

So XML is somewhere between a document and a relational-table. Imagine a database table where each record would have a very different structure, that would be good use for XML. Also XML is very good for data interchange, meanwhile files like .DBF, .XLS etc. are not so good.

#### What is CRUD?

In computer programming, create, read, update, and delete (as an acronym CRUD) are the four basic functions of persistent storage.

#### Primary key vs foreign key

A primary key, also called a primary keyword, is a key in a relational database that is unique for each record. It is a unique identifier, such as a driver license number, telephone number (including area code), or vehicle identification number (VIN). A relational database must always have one and only one primary key.

In the context of relational databases, a foreign key is a field (or collection of fields) in one table that uniquely identifies a row of another table or the same table. In simpler words, the foreign key is defined in a second table, but it refers to the primary key in the first table.

Example: there are two tables: one for first name and their ids, and second for adresses and ids. Then, we have another table that has reference from these two tables. Basically third table includes people id(ids comes from name table) and adress id(from adress table). So the ids of the first two tables are primary keys and the people ids and adress ids from the third table is the foreign key that refers to first two tables.

--------

## From [heroku documentation](https://devcenter.heroku.com/articles/sqlite3)

Ruby on Rails and some other web based frameworks ship with support for a small database called sqlite3 by default. SQLite is ideal for users getting started since it can be run in memory and backed by small files on disk that are easily created and moved around. While easy to use, SQLite is not intended as a production grade database. Instead Heroku provides production grade PostgreSQL databases as a service.

### Disk backed storage

SQLite runs in memory, and backs up its data store in files on disk. While this strategy works well for development, Heroku’s Cedar stack has an ephemeral filesystem. You can write to it, and you can read from it, but the contents will be cleared periodically. If you were to use SQLite on Heroku, you would lose your entire database at least once every 24 hours.

Even if Heroku’s disks were persistent running SQLite would still not be a good fit. Since SQLite does not run as a service, each dyno would run a separate running copy. Each of these copies need their own disk backed store. This would mean that each dyno powering your app would have a different set of data since the disks are not synchronized.

### Running Rails on Postgres

PostgreSQL database can be used by any language and framework, this section covers how to connect to it through the Ruby on Rails framework. It is important that you use the same database in production as in development, so you will need to install the PostgreSQL database locally.

> Did you get Postgres working locally? This is important. [install the PostgreSQL database locally](https://devcenter.heroku.com/articles/heroku-postgresql#local-setup)

- Check the[link](https://devcenter.heroku.com/articles/sqlite3#running-rails-on-postgres) to see how to change default db into Postgres.

### Getting a SQLite error even though it is not in the Gemfile

If you’ve removed the `gem 'sqlite3'` line from your `Gemfile` and are still getting errors while deploying to Heroku it is likely that another gem you are using has `sqlite3` as a dependency. To help find the source of this dependency look in your `Gemfile.lock` for `sqlite3`. Find the gem that has `sqlite3` as a dependency and remove it from your `Gemfile`. Once you’ve done this run `bundle install` and ensure that `sqlite3` no longer exists in your `Gemfile.lock`.

























