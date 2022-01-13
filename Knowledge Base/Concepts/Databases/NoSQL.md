# NoSQL 
###### *This example is based on the common **MongoDB** database*
Tags[^2] 

## TOC
- [Description](#Description)
- [NoSQL Injection](../../Vulnerabilities/NoSQL%20Injection.md)
- [SQL vs NoSQL](#SQL%20vs%20NoSQL)
- [Structure](#Structure)
- [Commands](#Commands)
	- [Command Usage](#Command%20Usage)

[^2]: #rdbms #nosql #sql #database #mongodb 

## Description
Where *SQL* databases are based on uniform structure and tabular based, *NoSQL* databases (aka "not only SQL") are non-tabular databases and store data differently than relational tables. NoSQL databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and graph. They provide flexible schemas and scale easily with large amounts of data and high user loads.

NoSQL databases are non-relational and come in a variety of formats[^1].

[^1]: https://www.mongodb.com/nosql-explained

-   **Document databases** store data in documents similar to JSON (JavaScript Object Notation) objects. Each document contains pairs of fields and values. The values can typically be a variety of types including things like strings, numbers, booleans, arrays, or objects.
-   **Key-value databases** are a simpler type of database where each item contains keys and values.
-   **Wide-column stores** store data in tables, rows, and dynamic columns.
-   **Graph databases** store data in nodes and edges. Nodes typically store information about people, places, and things, while edges store information about the relationships between the nodes.

In a document database, for example, a **collection** of users will contain various **documents** that contain various **fields** that contain **key-value** pairs used to store/access the data. 

## Injection
See [NoSQL Injection](../../Vulnerabilities/NoSQL%20Injection.md)

## SQL vs NoSQL

### Structure
In an RDBMS (relational database management system), data is modeled in tables. In *NoSQL*, data are likely stored as *objects* in a format such as `JSON`. A NoSQL database such as **MongoDB** will have collections, documents, and fields. 

In a situation where we want to store a database of *users* and *hobbies*,  the data will be stored differently depending on the type of database. 

In an *RDBMS*, we'd likely have two databases, one for each, in a relational database. Bringing the data together would require a join

**Users**

| ID | first_name | last_name | cell | city |
| :-: |  :-: |  :-: |  :-: |  :-: |
| 1 | Leslie | Yepp | 8168751 | Tulsa | 

**Hobbies**

| ID | user_id | hobby | 
| :-: | :-: | :-: | 
| 10 | 1 | scrapbooking | 
| 11 | 1 | eating burgers |
| 12 | 1 | working |

In a *NoSQL* database, the data model depends on the type of DB. In a *document database* like **MongoDB**, we'd store it in `JSON`. 

```
{ 
	"_id": 1, 
	"first_name": "Leslie", 
	"last_name": "Yepp", 
	"cell": "8125552344", 
	"city": "Pawnee", 
	"hobbies": ["scrapbooking", "eating waffles", "working"] 
}
```

*In comparing the two:*
- **Collections** are similar to tables or views in MySQL
- **Documents** are similar to rows or records in MySQL
- **Fields** are similar to columns in MySQL

### Commands
###### View a full list of MongoDB operators here &mdash; [MongoDB Query Reference] (https://docs.mongodb.com/manual/reference/operator/query/)
To start interacting with a local **MongoDB** server, simply type `mongo` or `mongosh`, the latter for improved usability and compatibility. The former will be deprecated on the next release. 

*Comparing basic operators in **MongoDB** to **MySQL:***
- `$and` equals `and`
- `$or` equals `OR`
- `$eq` equals `=`

*Common operators:*
- `$eq` - matches records that equal to a certain value
- `$ne` - matches records that are not equal to a certain value
- `$gt` - matches records that are greater than a certain value.
- `$where` - matches records based on Javascript condition
- `$exists` - matches records that have a certain field
- `$regex` - matches records that satisfy certain regular expressions.


*Basic usage:*
- `show databases` &mdash; list available databases
- `use` &mdash; to connect to an existing database or create a new one
- `db.getCollectionNames()` &mdash; lists all the collections in the current database. 
- `db.createCollection("COLLECTION_NAME")` &mdash; creates a new collection in the database we are connected to 
- `db.COLLECTION.insert({key:"value", key: "value", key: "value"})` &mdash; this function creates a document in whatever `COLLECITON` we entered with the command. 
- `db.COLLECITON.find("query")` &mdash; selects documents within `COLLECITON` that match the query, or finds all if empty
- `db.COLLECITON.update({key:'value"}, {$set: {key: "value"}});'` &mdash; within the chosen `COLLECITON`, find a document with a specific `key:value` pair and update the chosen `key` with a new `value` using the `$set` function. 
	- e.g., find an `_id` with the value `2` and update the `username` to `"admin2"` &mdash; `db.users.update({_id: "1"}, {$set: {username: "admin2"}})`
- `db.COLLECTION.remove({"query"})` &mdash; removes the selected `query`
- `db.COLLECTION.drop()` &mdash; ends the session with the current collection.

#### Command Usage
*Creating a DB and Collection*
- `use test_db;`
- `db.createCollection("test_users")`

![Creating DB and Collection](Photos%20(Concepts)/NoSQL-Creating-DB-and-Collection.png)

*Creating and Finding Documents*
- `db.test_users.insert({id:"1", username: "admin", email: "n0_ware@hacks.io", password: "badpass123"})`
- `db.test_users.insert({id:"2", username: "lowpriv", email: "easy@target.io", password: "passpass"})`
- `db.test_users.find()`

![Creating and Finding Documents](Photos%20(Concepts)/NoSQL-Creating-and-Finding-Documents.png)

*Updating a Document*
- `db.test_users.update({id:"2"}, {$set: {username: "harder_target", password: "AmucHb3tt3rp4ssw0rd!##&"}});
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })`

![Updating a Document](Photos%20(Concepts)/NoSQL-Update-a-Document.png)


*Finding a Specific Document*
- `db.test_users.find({id:"2"})`

![Finding a Specific Document](Photos%20(Concepts)/NoSQL-Finding-A-Specific-Document.png)

*Remove a Document*
- `db.test_users.remove({id:"2"})`

![Remove a Document](Photos%20(Concepts)/NoSQL-Remove-a-Document.png)


#### Query Structure

When using a query in a *NoSQL* command, you can simply provide the exact document you are looking for via a `key`, typically the `id`, such as with `{id: "1"}` to return the document with the `id` equal to one. 

However, you can use various commands in the query structure to get different results. When doing so, wrap the query in `{}` inside of the value you are searching for. For example, if we wanted all documents with an `id` less than `3`, we would use a query such as `db.test_users.find({id:{"$lt" : "3"}})`. The structure of a query goes like this:
- `{Key:{"$operator" : "value"}})`