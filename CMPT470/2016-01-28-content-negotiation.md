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

# NoSQL

> a general term for modern non-relational databases.
  * doesn't describe a technology, or even specific type

*Motivation*: very high volume sites with huge data stores.
* Then the relational/SQL/ACID paradigm is **slow**.
* Hard to be consistent across many servers
* joins can be expensive with lots of data.
* ACID guarantees can be unnecessary.
  * maybe we don't care about occasional missed transactions
  * bank: definitely do care
  * up/downvotes on comments: whatever
  * post not globally-visible for
* NoSQL DBs also have simpler data models
  * e.g. key/value store
  * e.g. document store: each row is like a JSON object of key/value pairs
* ACID rules can be relaxed.
  * e.g. eventual consistency: multiple servers may have different data temporarily, but will sync soon.
  * e.g. restrict what is a **transaction**.
* many different techs described as **NoSQL**
  * different tradeoffs of various DB properties
  * goal is generally speed/scalability
  * maybe need multiple DB techs for your system.
* but...
  * modern relational databases are very fast and can hold huge amounts of databases
  * why make life more complicated if Postgres will do the job?
  * some NoSQL databases are *immature*.
* suggestions
  * think of NoSQL as an optimization
  * using as a cache can be very effective (memcached, Redis)

## Summary

* there's more to data storage than relational + ACID.
* some data is better suited to other tools

# Model View Controller (MVC)

> Model/View/Controller architecture

* **Model**: the data layer
  * holds the info & the logic to manipulate it.
  * usually classes/objects for the data you've got.
  * often combined with an ORM
  * good OO and/or relational DB design should take care of it
* **View**: display
  * arranges data for the user to see
  * *for the web*: usually HTML templates.
  * **should contain no (significant) logic** -- that goes in M/C
* **Controller**: responds to events (user actions)
  * HTTP requests for web
  * uses the model to get the data, and view to present to user
* many web frameworks use MVC (terms may vary)
