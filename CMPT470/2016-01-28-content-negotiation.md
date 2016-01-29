# Content Negotiation

* `Accept`:
* `Accept-language`:
* `Accept-charset`: `utf-8, *;q=0.6`
  * character encoding
  * *but of little use*
* `Accept-encoding`: `gzip, deflate`
  * how can data be encoded for transport?
  * allows compression that's invisible to the user.
  * server can compress the resource, but could ignore if it makes sense.
* for static content:
  * in *Apache*, either multi-views or type maps to indicate file variants
  most servers can at least compress static content, if turned on.
* for dynamic content, up to the programmer.
  * most frameworks have some support for **language negotiation (i18n)** and **compression**

# Relational Databases

* a relational DB is very useful for data storage in a web app
  * fast at retrieving info
* many open source servers
* indexes/keys are important

## Relational DB Servers

* many choices:
  * the free ones: `MySQL`,`Postgres`, `SQLite`, `MariaDB`
  * the expensive ones: `Oracle`, `DB2`
  * others: `Cassandra`, `Mongo`
* for web work, free and relational is good default

### MySQL/MariaDB

* well proven, very commonly used, fast.

### Postgres

* also well proven
* better transactions, more data types

### SQLite
* your "database" is just a file
* great for development
* probably not right for production

## Object-Relational Mapping

* *actually* writing a lot of SQL is a pain
* most DB activity is similar:
> load and store database
> that are linked by primary key
> and could be represented by objects
> and have artificial primary keys

* an object's properties often map closely to a table's columns
  * class `Person` has `fname`,`lname`
  * table `people` has columns: `fname`,`lname`
  * converting is a lot of boring work
* an **object-relational mapper** connects objects and DB tables automatically

  Lets us write code like

  ```python

  p = new Person()
  p.fname = "John"
  p.save()
  p.lname = "Smith"
  p.save()
  people = Person.select(fname="John")
  ```

  No need to write SQL.

* ORMs can also handle relationships

  e.g. a person has many books, then we expect something like

   ```python
   book = (something)
  book.person.fname == "John"
   ```
  
