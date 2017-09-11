
All slides on [Github](https://aelavender.github.io/intro-to-sql-2):

https://aelavender.github.io/intro-to-sql-2


:note:

Speaker notes start with the line as above

Separate slides with a blank line, then 3 hyphens, then another blank line, as in the line below.

---

# Intro to SQL

#### a.e. Lavender [@\_\_metaclass\_\_](https://twitter.com/__metaclass__)

Based on original content by Vicki Boykis [@vboykis](https://twitter.com/vboykis)

---

## Welcome!

Girl Develop It is here to provide affordable and accessible programs to learn software through mentorship and hands-on instruction.

[Our code of conduct](https://www.girldevelopit.com/code-of-conduct)

Some rules:
- We are here for you!
- Every question is important
- Help each other
- Have fun

---

## Tell us about yourself.
- Who are you?
- What's your experience level with SQL?
- What do you hope to get out of the class?
- How many other GDI classes have you taken?
- What is your favorite movie, and how many times have you watched it?

---

## About me
- Software architect / data engineer at [Monetate](http://www.monetate.com) (We're hiring!)
- 10 years of experience with SQL
- Favourite movie is Princess Mononoke. I've seen it about 8 times.

---

## What to expect
- This is a complement to Sondre's database design class
  - You don't have to have taken that class in order to make use of SQL
  - Same terminology
  - Less theory, more practice

---

## What to expect
- Goals: By the end of this class you will be able to:
  - Query, filter, group, and aggregate data from a database table
  - Join multiple tables together to take advantage of relationships between tables
  - Add, update, and remove data from a database

---

## Plan for the day
- What's a database? What's SQL?
- Getting data out of a database (about 3/4 of the class):
  - `SELECT ... FROM ...`
  - Selecting distinct and counting elements
  - Filtering: `WHERE`
  - Ordering: `ORDER BY`
  - Aggregation functions
  - Grouping: `GROUP BY`

---

## Plan for the day
- Getting data out of a database (continued):
  - Joining multiple tables together: `JOIN`
  - Sub-queries
- Updating data in a database:
  - Adding a row to a table: `INSERT`
  - Modifying rows: `UPDATE`
  - Removing rows: `DELETE`
- Updating the structure of the database itself
  - Data types
  - Creating tables
- Big Data, NoSQL, and alternative models

---

## What's a Relational Database?
- A relational database management system (RDBMS) is a way of storing data using the "relational data model"
  - Data is stored in tables
  - Tables have well-defined relationships between them
- The most common type of database today; when people just say "database," they almost always mean "relational database."
- Examples: Oracle, MS SQL Server, MySQL, Postgres, SQLite

---

## Terminology
- *Database System*: The hardware and software hosting the data
  - Typically runs on a server
  - A database system hosts one or more schemata.
- *Schema*: The layout of your data:
  - The names and structures of your tables and the relationships between them
  - A schema holds one or more tables.

---

## Terminology
- *Table*: A collection of records that all have the same structure
  - A table has many rows and many columns.
- *Column*: The structure of your table
  - Each column has a _name_ and a _type_
- *Row*: A single record of data: a singe "object" or "element"
  - Each row has one value for each column in the table.
- *Value*: A single piece of data (number, string, date, etc)

---

## Compared to Excel

| Database | Excel     |
| -------- | --------- |
| Schema   | Workbook  |
| Table    | Worksheet |
| Row      | Row       |
| Column   | Column    |
| Value    | Cell      |

---

## Differences from Excel
- Database columns have *names* (e.g. `UserName`) instead of letters (A, B, C, ...)
- Database columns have *types* (numbers, strings, dates)
- Database rows have *Primary Keys* instead of numbers (1, 2, 3, ...)
- Database tables hold just data (values), not formulas
  - Use SQL instead of formulas!
- Database tables can be *joined*
  - like `vlookup` but more powerful!

---

## What's SQL?
- Stands for Structured Query Language
- How to ask ("Query") a database for information
- A "declarative" language: ask for what you want; the database figures out how to get it.
- Nobody pronounces it correctly
- Each database system uses a slightly different "flavour" of SQL

---

## The "Structure" in SQL:

Example of SQL Select statement:

```sql
SELECT UserName, SUM(PurchaseAmount) as Total
FROM billing_database.purchases
WHERE PurchaseDate >= '2017-01-01'
  AND ProductCategory = 'books'
  AND UserName like 'Alice%'
GROUP BY UserName
HAVING Total > 50.00
ORDER BY Total DESC
LIMIT 100;
```

What do you think this statement does?

---

## The Select Statement

##### Use these words, in this order:

- `SELECT`: What data (columns) do you want? (required)
- `FROM`: Which table(s) do you want it from? (required)
- `WHERE`: Filter which rows to return
- `GROUP BY`: Groups rows together
- `HAVING`: Filter which groups to return
- `ORDER BY`: Sort results
- `LIMIT`: How many results to return? (MySQL-specific!)

---

## Let's get connected!

TODO Add connection info and image here

---

## About our data

This is _real data_ from [Stack Overflow](https://data.stackexchange.com)!

- Stack Overflow is a Q&A website.
- Users can create post questions and answers to those questions
- Questions can be tagged with categories
- Users can vote on both questions and answers
  - The number of Upvotes and Downvotes result in a question or answer's "score"
  - The person who asked the question can choose which response best answered the question
  - Users gain "reputation" for getting upvoted and for getting their answer accepted


---

## Our very first SQL statement!

```sql
SELECT * FROM stackoverflow.Users;
```

:note:

Is SQL case sensitive?  It depends on what kinda SQL.
  - Keywords are usually NOT case sensitive
  - Table and column names usually ARE case sensitive
  - Data can go either way...

At this point, switch to Workbench and do it interactively.

---

#### Let's try a few modifications...

```sql
SELECT * FROM stackoverflow.Users
LIMIT 10;
```
<!-- .element: class="fragment" -->

```sql
SELECT DisplayName, Location, Age
FROM stackoverflow.Users;
```
<!-- .element: class="fragment" -->

```sql
SELECT DisplayName, Location, Age
FROM stackoverflow.Users
LIMIT 10;
```
<!-- .element: class="fragment" -->

```sql
SELECT COUNT(*) FROM stackoverflow.Users;
```
<!-- .element: class="fragment" -->

---

#### Let's take some time to explore some of the other tables...
```sql
SELECT * FROM stackoverflow.Tags LIMIT 10;

SELECT * FROM stackoverflow.Votes LIMIT 10;

SELECT * FROM stackoverflow.Posts LIMIT 10;
```
This is a great way to explore a new dataset and see what kind of data you've got.

---

#### We can already do some useful things!

```sql
-- How many users do we have?
SELECT COUNT(*) FROM stackoverflow.Users;

-- How many posts have been made so far?
SELECT COUNT(*) FROM stackoverflow.Posts;

-- This is how you write a comment in SQL, btw...
```

---

## Stretch Break!

:note:

After the stretch break, briefly mention the following:
- Specifying the schema (stackoverflow) in front of every table name is not necessary but good practice
- The semi-colon is not necessary if you only have one statement but useful to separate multiple statements

---

## Filtering: The `WHERE` clause

What if we only want to see Users who have a Reputation of at least 1000?

```sql
SELECT * FROM stackoverflow.Users
WHERE Reputation >= 1000;
```

---

#### Try answering these questions!

- Get all users under the age of 30
- What's user `dba4life`'s website?
- Get the names of users who are from Philadelphia, PA
- Get the ID numbers and creation dates of all users who joined the site since January 1, 2017
- _How many_ users have reputation of at least 1000?  At least 5000?
- _How many_ users haven't filled out their "About Me" section yet?

**If you're not sure if something will work, try it and see! Don't worry if you can't get all of these!**

--

#### Get all users under the age of 30
```sql
SELECT * FROM stackoverflow.Users
WHERE Age < 30;
```

--

##### What's user `dba4life`'s website?
```sql
SELECT WebsiteUrl
FROM stackoverflow.Users
WHERE DisplayName = 'dba4life';
```
Note that strings must be `'quoted like this'`

--

##### Get the names of users who are from Philly
```sql
SELECT DisplayName FROM stackoverflow.Users
WHERE Location = 'Philadelphia, PA';
```

--

##### Get the ID numbers and creation dates of all users who joined the site since January 1, 2017

```sql
SELECT Id, CreationDate
FROM stackoverflow.Users
WHERE CreationDate >= '2017-01-01';
```

Dates need to be quoted and formatted like this: `'2017-01-01'`

--

##### How many users have reputation of at least 1000?
```sql
SELECT COUNT(*)
FROM stackoverflow.Users
WHERE Reputation > 1000;
```
##### At least 5000?
```sql
SELECT COUNT(*)
FROM stackoverflow.Users
WHERE Reputation > 5000;
```

--

#### _How many_ users haven't filled out there "About Me" section yet?

```sql
SELECT COUNT(*)
FROM stackoverflow.Users
WHERE AboutMe IS NULL;
```

- `NULL` is a special value in SQL
- You can filter by `IS NULL` or `IS NOT NULL`
- Note that `WHERE AboutMe = NULL` doesn't work!

---

#### More things you can do with `WHERE`

- Which users have given out more DownVotes than UpVotes?
- Which users have a reputation of at least 1000 _and_ have been viewed at least 100 times?
- Get me the names of the users with the following ID numbers: 45194, 99717, and 108803.

--

```sql
-- More downvotes than upvotes:
SELECT * FROM stackoverflow.Users
WHERE DownVotes > UpVotes;

-- High reputation and many views:
SELECT * FROM stackoverflow.Users
WHERE Reputation >= 1000
AND Viewed >= 100;

-- A set of specific ID numbers
SELECT * FROM stackoverflow.Users
WHERE Id IN (45194, 99717, 108803)
```

:note:

Have students try these first.

New concepts introduced:
- WHERE can compare two different columns, not just a column with a constant
- Multiple conditions with AND / OR
- The IN operator is equivalent to a bunch of equal clauses

---

#### Which users are from Philly again?

Previously we did something like this...

```sql
SELECT * FROM stackoverflow.Users
WHERE Location = 'Philadelphia, PA';
```


But what if we did this instead...
<!-- .element: class="fragment" data-fragment-index="1"-->


```sql
SELECT * FROM stackoverflow.Users
WHERE Location LIKE 'Philadelphia%';
```
<!-- .element: class="fragment" data-fragment-index="1"-->


<!-- .element: class="fragment"-->`LIKE` is a pattern-matching operator.  The `%` character is a wildcard and can go anywhere in the pattern.

---

## Stretch Break!

---

## Putting things in `ORDER`:

```sql
SELECT * FROM stackoverflow.Users
ORDER BY DisplayName;
```

---

Our top 10 users with the highest reputation:

```sql
SELECT * FROM stackoverflow.Users
ORDER BY Reputation DESC
LIMIT 10;
```

Our 10 most recently joined users:

```sql
SELECT * FROM stackoverflow.Users
ORDER BY CreationDate DESC
LIMIT 10;
```

What if I wanted the 10 most recent users _from Philly_?

How do I get the 10 youngest users?

--

```sql
-- 10 most recent from Philly
SELECT * FROM stackoverflow.Users
WHERE Location like 'Philadelphia%'
ORDER BY CreationDate DESC
LIMIT 10;

-- 10 youngest
SELECT * FROM stackoverflow.Users
WHERE Age IS NOT NULL
ORDER BY Age ASC
LIMIT 10;
```

---

You can `ORDER BY` multiple columns, in different directions:
```sql
SELECT * FROM stackoverflow.Users
ORDER BY Views ASC, UpVotes DESC, LastAccessDate DESC;
```

---

## Aggregation functions

Aggregation functions collapse and summarise your data.

You've already seen one aggregation function, `COUNT`:
```sql
SELECT COUNT(*) FROM stackoverflow.Users;
```

If you give it a column name, it can do even more:
<!-- .element: class="fragment" -->

```sql
SELECT COUNT(Location) FROM stackoverflow.Users;

SELECT COUNT(DISTINCT Location)
FROM stackoverflow.Users;
```
<!-- .element: class="fragment" -->

You can combine those last two queries:
<!-- .element: class="fragment" -->

```sql
SELECT COUNT(Location), COUNT(DISTINCT Location)
FROM stackoverflow.Users;
```
<!-- .element: class="fragment" -->

---

##### There are more aggregation functions:

Minumum, Maximum, Sum, Average

```sql
SELECT
  MIN(Reputation),
  MAX(Reputation),
  SUM(Reputation),
  AVG(Reputation)
FROM stackoverflow.Users;
```

And we can use `WHERE` as well:

```sql
SELECT
  MIN(Reputation),
  MAX(Reputation),
  SUM(Reputation),
  AVG(Reputation)
FROM stackoverflow.Users
WHERE CreationDate >= '2017-01-01';
```

---

## Aggregations are more fun with `GROUP BY`

How many users do I have in each location?

```sql
SELECT Location, COUNT(*)
FROM stackoverflow.Users
GROUP BY Location;
```
<!-- .element: class="fragment" -->

---

##### Try these:
- How many users under 30 are in each location?
- Which locations have the highest average reputation?
- Do any users have the same Display Name? Do any have the same ID?

--

How many users under 30 are in each location?
```sql
SELECT Location, COUNT(*)
FROM stackoverflow.Users
WHERE Age < 30
GROUP BY Location;
```

--

Which locations have the highest average reputation?
```sql
SELECT Location, AVG(Reputation)
FROM stackoverflow.Users
GROUP BY Location
ORDER BY AVG(Reputation) DESC;
```

I could have saved some typing by using an _alias_:
```sql
SELECT Location, AVG(Reputation) AS AvgRep
FROM stackoverflow.Users
GROUP BY Location
ORDER BY AvgRep DESC;
```

This will come in handy later...

--

Names in common
```sql
SELECT DisplayName, count(*)
FROM stackoverflow.Users
GROUP BY DisplayName
ORDER BY count(*) DESC;
```
Does this result surprise you?

:note:

Aliases -- the `AS` is not necessary but makes things clearer

Names in common -- ID is a primary key and therefore unique. DisplayName is NOT a primary key. Keep that in mind when we start talking about joins.

---

## LUNCH!

---

## Joins

Let's take a peak at the Comments table.

```sql
SELECT * FROM stackoverflow.Comments limit 10;
```

What do you suppose the `UserId` column means?

<div class="fragment">
This is a _reference_, also known as a _foreign key_.  It "points at" another table (in this case, the `Users` table).

Wouldn't it be nice if we could combine them?
</div>

---

##### Our First Join:  Comments with Users
```sql
SELECT *
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id;
```

:note:

A ton of new things here, so let's walk through it slowly.

- `SELECT *` looks familiar, but since we're getting data from two tables, it gives us all of the columns from both tables
- Using aliases for the tables. This is not necessary -- I could have written out the names every time -- but very useful.
- `ON`: This is the "join condition". We're gluing two tables together, and this specifies how to match things up. In the case, we want `UserId` from the Comments table to match with `Id` from the Users table. Let's look at the results and see that this is indeed the case.
- `INNER JOIN`: The default and most common kind of join.
  - If you had just said `JOIN` then SQL assumes you mean `INNER JOIN`. I like to write it out in full for clarity.
  - It means find every case where the join condition matches, and if a row in either table doesn't match then don't include it. (We'll talk about other types of joins in a bit.)
- Let's look at the results. A few things to note:
  - Multiple columns called ID, and they are different. SELECT Id FROM ... won't work; need to use the alias.
  - Rows from the Users table can appear more than once. Why?
  - Do any rows from the Comments table appear more than once? How do we know?

---

#### `WHERE`, `GROUP BY`, and `ORDER BY` still work

But you have to be careful when specifying columns. I like to _always_ include the table alias for clarity.

What does this do?

```sql
SELECT
  c.Text, u.DisplayName
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id
WHERE
  c.CreationDate >= '2017-01-01'
  AND u.Reputation >= 1000
  AND c.Text LIKE '%mysql%'
ORDER BY
  c.CreationDate DESC;
```

:note:

Get Comment text and name of commenter for all comments made after 2017-01-01 from users with reputation > 1000 with the word 'mysql' in them, sorted newest comments first.

---

#### Try answering these!

- How many comments were made by users from Philadelphia? What was the highest score amongst these comments?
- Which 10 users have made the most comments?
- Amongst users who joined this year, which user has made the most comments?
- What is the total Score of comments by Age?

--

Comments from Philly:
```sql
SELECT
  COUNT(*) as cnt,
  MAX(c.Score) as highest_score
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id
WHERE u.Location LIKE 'Philadelphia%';
```

--

Comments from Philly:
```sql
SELECT
  COUNT(*) as cnt,
  MAX(c.Score) as highest_score
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id
WHERE u.Location LIKE 'Philadelphia%';
```

--

Users with most comments:
```
SELECT u.Id, u.DisplayName, COUNT(*) AS cnt
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id
GROUP BY u.Id, u.DisplayName
ORDER BY cnt DESC
LIMIT 10;
```

--

User who joined this year with most comments:
```
SELECT u.Id, u.DisplayName, COUNT(*) AS cnt
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id
WHERE u.CreationDate >= '2017-01-01'
GROUP BY u.Id, u.DisplayName
ORDER BY cnt DESC
LIMIT 1;
```

--

Scores by age
```sql
SELECT u.Age, SUM(c.Score) AS TotalScore
FROM stackoverflow.Comments AS c
INNER JOIN stackoverflow.Users AS u
  ON c.UserId = u.Id
GROUP BY u.Age
ORDER BY TotalScore DESC;
```

---

## Joins are cool! What else can we join?

TODO: Insert schema diagram here

:note:

- The arrows represent foreign key relations -- where a column in one table references the id of another table.
- In this schema, Primary Keys are always called 'ID'. This is a convention (and a very common one) but it won't always be the case.
- Whats with the 'Types' tables?
- What's the deal with the Posts table pointing to itself?
  - Posts contains both questions and answers.
  - Answers have a ParentID which points to the question they are answering
  - Questions have an AcceptedAnswerId which points to the Answer that the questioner chose as best
  - (Work through an example -- number of answers given for each question)
- What's with the PostTags table? Why is this necessary?
  - It's called a "Through Table" and is necessary to represent a many-to-many relation: a Post can have many Tags, and a Tag can be applied to many Posts

---

#### Try these!

- Which users have asked the most questions?
- Which users have answered the most questions?
- How many questions have been tagged with 'mysql'?
- Which tag has been used the most?
- How many votes of each type have been cast?
- Which questions have had the most UpVotes?
- Get a list of questions and answers where the user answered their own question.
- Which users have the most Accepted answers?

--

Which users have asked the most questions?
```sql
SELECT
  u.Id,
  max(u.DisplayName) AS name,
  COUNT(*) AS
FROM stackoverflow.Users u
INNER JOIN stackoverflow.Posts q
  ON u.ID = q.OwnerId
INNER JOIN stackoverflow.PostTypes pt
  ON q.PostTypeId = pt.Id
WHERE pt.name = 'Question'
GROUP BY u.Id
ORDER BY cnt DESC
```
How do I change this to get users who have answered the most questions?

--

Which users have answered the most questions?
```sql
SELECT
  u.Id,
  max(u.DisplayName) AS name,
  COUNT(*) AS
FROM stackoverflow.Users u
INNER JOIN stackoverflow.Posts q
  ON u.ID = q.OwnerId
INNER JOIN stackoverflow.PostTypes pt
  ON q.PostTypeId = pt.Id
WHERE pt.name = 'Answer'
GROUP BY u.Id
ORDER BY cnt DESC
```

--

How many questions have been tagged with 'mysql'?
```sql
SELECT *
FROM stackoverflow.Posts AS q
INNER JOIN stackoverflow.PostTypes AS pt
  ON q.PostTypeId = pt.Id
INNER JOIN stackoverflow.PostTags
WHERE pt.Name = 'Question'

--

Which tag has been used the most?
```sql
SELECT t.TagName, count(*) AS cnt
FROM stackoverflow.Tags t
INNER JOIN stackoverflow.PostTags AS pt
  ON t.Id = pt.TagId
GROUP BY t.TagName
ORDER BY cnt DESC;
```

--

How many votes of each type have been cast?
```sql
SELECT vt.Name, COUNT(*) AS cnt
FROM stackoverflow.Votes AS v
INNER JOIN stackoverflow.VoteTypes AS vt
  ON v.VoteTypeId = vt.Id
GROUP BY vt.Name
ORDER BY cnt DESC;
```

--

Which questions have had the most UpVotes?
```sql
SELECT p.Id, p.Title,
  COUNT(*) as cnt_upvotes
FROM stackoverflow.Posts AS p
INNER JOIN stackoverflow.PostTypes AS pt
  ON p.PostTypeId = pt.Id
INNER JOIN stackoverflow.Votes AS v
  ON p.Id = v.PostId
INNER JOIN stackoverflow.VoteTypes AS vt
  ON v.VoteTypeId = vt.Id
WHERE pt.Name = 'Question'
  AND vt.Name = 'UpVote'
GROUP BY p.Id
ORDER BY cnt_upvotes DESC
LIMIT 100;
```

--

Get a list of questions and answers where the user answered their own question.
```sql
SELECT u.Id, u.DisplayName, q.Title,
  q.Body AS question_body,
  a.Body AS answer_body
FROM stackoverflow.Posts AS q
INNER JOIN stackoverflow.Posts AS a
  ON q.Id = a.ParentId
INNER JOIN stackoverflow.Users AS u
  ON q.OwnerUserId = u.Id
WHERE q.OwnerUserId = a.OwnerUserId;
```
How would I change this to get instances where the user _accepted_ their own answer?

--

Which users have the most Accepted answers?
```sql
SELECT u.Id, u.DisplayName,
  COUNT(*) as cnt_accepted_answers
FROM stackoverflow.Posts AS q
INNER JOIN stackoverflow.Posts AS a
  ON q.AcceptedAnswerId = a.Id
INNER JOIN stackoverflow.Users AS u
  ON a.OwnerUserId = u.Id
GROUP BY u.Id
ORDER BY cnt_accepted_answers desc;
```

---

## STRETCH BREAK!

:note:

Leave an hour for insert/update/delete, summary, and wrap-up. Omit or shorten sections on subqueries, outer joins, and HAVING if necessary to make sure students understand inner joins.

TODO: Sub-queries

TODO: Start writing Intermediate SQL course :-)

---

## HAVING: Filtering _after_ grouping

Which users have answerd at least 100 questions this year?  (Let's say thanks!)
```sql
SELECT u.Id, u.DisplayName,
  COUNT(*) as questions_answered
FROM stackoverflow.Users AS u
INNER JOIN stackoverflow.Posts AS p
  ON u.Id = p.OwnerUserId
INNER JOIN stackoverflow.PostTypes AS pt
  ON p.PostTypeId = pt.Id
WHERE pt.Name = 'Answer'
  AND p.CreationDate >= '2017-01-01'
GROUP BY u.Id
HAVING questions_answered >= 100;
```
<!-- .element: class="fragment" -->

---

#### Try these!
- Which questions have at least 4 tags?
- Which questions have only one answer so far?

--

Which questions have at least 4 tags?
```sql
SELECT p.Id, p.Title, COUNT(*) AS cnt_tags
FROM stackoverflow.Posts AS p
INNER JOIN stackoverflow.PostTypes AS ptypes
  ON p.PostTypeId = ptypes.Id
INNER JOIN stackoverflow.PostTags AS ptags
  ON p.Id = ptags.PostId
WHERE ptypes.Name = 'Question'
GROUP BY p.Id
HAVING cnt_tags >= 4;
```

--

Which questions have only one answer so far?
```sql
SELECT q.Id, q.Title
FROM stackoverflow.Posts AS q
INNER JOIN stackoverflow.Posts AS a
  ON q.Id = a.ParentId
GROUP BY q.Id
HAVING COUNT(*) = 1;
```

---

## OUTER JOIN: What if there are no matches?

How many questions have no answers yet?  Perhaps you'd like to answer one!

Note: This is an advanced topic. Don't worry if you don't understand it yet!
```sql
SELECT q.Id, q.Title
FROM stackoverflow.Posts AS q
INNER JOIN stackoverflow.PostTypes AS pt
  ON q.PostTypeId = pt.Id
LEFT OUTER JOIN stackoverflow.Posts AS a
  ON q.Id = a.ParentId
WHERE pt.Name = 'Question'
GROUP BY q.Id
HAVING COUNT(a.Id) = 0;
```
<!-- .element: class="fragment" -->

:note:

Start with answer to previous question. Why doesn't it work to just change `HAVING COUNT(*) = 1` to `= 0`?

---

Try these!

- How many users have not made a post yet?

```sql
SELECT count(*)
FROM stackoverflow.Users AS u
LEFT OUTER JOIN stackoverflow.Posts AS p
   ON u.Id = p.OwnerUserId
WHERE p.Id is NULL;
```
<!-- .element: class="fragment" -->

---

## How does the data get there in the first place?

:note:

Often you won't have permission to modify data, and usually you won't want to.

---

## CRUD:
### Not as gross as it sounds

- **C**reate -- adding new data
- **R**etrieve -- we've learned this part!
- **U**pdate -- modifying data that already exists
- **D**elete -- removing data

---

## `INSERT`ing new data

Remember at the beginning of the class when you introduced yourself?

Let's put that information into a table!

```sql
select * from gdi.Students;
```
<!-- .element: class="fragment" -->

```sql
INSERT INTO gdi.Students
  (Name, ClassesTaken, FavouriteMovie, TimesSeen)
VALUES
  ('Lavender', 6, 'Princess Mononoke', 8);
```
<!-- .element: class="fragment" -->

:note:
Have student's insert their own data, then select to verify that it made it in there.

How did ID get there? It's an "auto-incrementing primary key"

Have each student figure out what their id number is.

---

## Now let's `UPDATE` your row!

Say I just watched _Princess Mononoke_ again over the lunch break. Now my table is out of date. Let's fix it.

```sql
UPDATE gdi.Students
SET TimesSeen = 9
WHERE Id = 1;
```
<!-- .element: class="fragment" -->

Why didn't I do it this way?<!-- .element: class="fragment" -->

```sql
UPDATE gdi.Students
SET TimesSeen = 9
WHERE Name = 'Lavender';
```
<!-- .element: class="fragment" -->

:note:

Have students update their row similarly.

---

#### Everyone here is just about to finish this GDI class, so let's give everyone credit!

```sql
UPDATE gdi.Students
SET ClassesTaken = ClassesTaken + 1

-- No WHERE clause, so do it for every row
```
<!-- .element: class="fragment" -->

---

## `DELETE` your data

What if you don't want to be in my table at all?

```sql
DELETE FROM gdi.Students
WHERE Id = 1;
```
<!-- .element: class="fragment" -->

---

What does this do?

```sql
DELETE FROM gdi.Students
WHERE Name LIKE 'L%';
```

What about this?

```sql
DELETE FROM gdi.Students;
```

---

## How did the _table_ get there in the first place?

```sql
SHOW CREATE TABLE gdi.Students;
```

:note:

This shows the CREATE TABLE statement that was used to create the table.
I can't run it again, since a table with that name already exists, but I can create a _new_ table just like it.

What do the various data types mean?

---

## SQL and the modern world

- Relational databases have been around since the 1970s and is still the most widely used type of database
  - Virtually all billing, banking, and e-commerce systems use SQL
  - Salesforce, Tableau, WordPress, Wikipedia
- More recently (within the last 10 years or so), "Big Data" and "NoSQL" have become popular
  - _Sometimes_ better for specific uses

---

## Alternatives to the Relational Model

---

#### Key-value stores
- Example: Redis
- Just like it sounds: everything has a unique key and an associated value
  - Values have no defined structure
  - There's no real WHERE or GROUP BY
- Good for: Distributed caches; key management; networking; image stores
- Bad for: business analysis, highly-structured data

---

#### Document Databases
- Example: MongoDB
- Store data as self-contained JSON
- Good for: Hierarchical data (e.g. a question having many comments and answers); loosely-schematised data (objects have some fields, but mabye not all, in common)
- Bad for: Relational data (Joins are hard!); data that gets updated frequently

---

#### Full-text Databases
- Example: Elasticsearch
- Similar to document databases, but with "textual analysis" features
- Good for: Text data, search engines, natural language processing
- Bad for: Numerical data; frequently updated data; your IT budget

---

#### Graph Databases
- Example: Neo4j
- Focus on relationships between objects: everything is a Join
- Good for: highly relational data (social networks; gene analysis)
- Bad for: simple data

---

#### MapReduce
- Example: Hadoop
- Not really a database -- more like a way to churn through a whole bunch of data.  Think if it as a massive `GROUP BY`.
- Good for: "Big Data"; statistical analysis and machine learning
- Bad for: Data consistency; selecting single items; small data

---

## What's old is new again

- Many non-relational databases implement SQL or a SQL-like language on top of their native functionality
  - Ex: Hive; SparQL
  - SQL is well-understood by many people
  - SQL statements are usuall shorter than the equivalent native language, but it can't do _everything_.
  - Combine SQL with native language to get best of both worlds

---

## Summary

#### Here's what we learned!

- Getting data out of your tables with `SELECT`
  - Counting rows; filtering; ordering
  - Grouping and aggregating
  - Joining tables together
- Modifying your data with `INSERT`, `UPDATE`, and `DELETE`

---

## What's next?
- More things you can do with joins and subqueries
- More SQL functions and expressions
- Structuring your data efficiently (Sondra's Database Design class)
- Modifying data safely: Transactions, constraints, ACID compliance
- Saving and sharing your SQL: Views, Triggers, and Stored Procedures
- Combining SQL with other programming languages
