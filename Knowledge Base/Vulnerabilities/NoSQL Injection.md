# NoSQL Injection
Tags[^1]

[^1]: #nosql #injection #webapp #query  #mongodb

## TOC
- [Description](#Description)
- [Examples](#Examples)
	- [Common Injection Operators](#Common%20Injection%20Operators)
	- [Bypassing Logins](#Bypassing%20Logins)
## Description
A web security vulnerability that allows attackers to control a [NoSQL](NoSQL.md) database, usually the result of unfiltered and untrusted [user supplied input](../Concepts/Web/User-Supplied%20Input.md) through an application. This can lead to unauthorized information disclosure and/or the alteration of a database.

## Examples

### Entry Point
The key to any injection is finding an unsanitized entry point, such as a URL bar.

For example, if you can read a NoSQL query in a URL, you know that you can inject at that point. 

### Common Injection Operators

*The below are often used to abuse queries:* 
- `$eq` - matches records that equal to a certain value
- `$ne` - matches records that are not equal to a certain value
- `$gt` - matches records that are greater than a certain value.
- `$where` - matches records based on `Javascript` condition
- `$exists` - matches records that have a certain field
- `$regex` - matches records that satisfy certain regular expressions.

###### View a full list of MongoDB operators here &mdash; [MongoDB Query Reference] (https://docs.mongodb.com/manual/reference/operator/query/)

### Bypassing Logins
Login page logic is similar in most databases. 
- First, connect to the database
- Then, look for the supplied `username` and see if it matches the supplied `password`. 
- If this evaluates to true, then the entry is valid and the login is granted.

An example evaluated to true [query](../Concepts/General/Queries.md) may be:

```
> db.users.findOne({username: "admin", password: "adminpass"}) 

{ 
	"_id" : ObjectId("1183af4b61de7a3d75f0c81f"), 
	"id" : "1", 
	"username" : "admin", 
	"email" : "n0_ware@hacks.io", 
	"password" : "adminpass" 
}
```

If the query is sent to the DB returns `true` it is successful and the server responds with  `JSON` back. If not, we get a `null` value.

***Remember, all we need to do is have the query evaluate to `true`, and without proper filtering, this can easily be accomplished.***

In the above example, we can still evaluate to `true` with the user `admin` if the `password` key itself provides a true value. 

Replacing `adminpass` with the statement `{"$ne": "xyz"}` tells the database to return a document (the user `admin`) with a password that is `not equal` to `xyz`. In our case, this is true, because the password `is not` equal to `xyz` for `admin`. 

This same concept is applicable to the `username` field. Consider this as well, which wil log us in to the first available user that `is not` admin and has a password `not equal` to `xyz` &mdash; `db.users.findOne({username:{"$ne":"admin"}, password:{} "$ne":"xyz"}})`

It is up to you to identify where the injection can take place, such as in the URL bar or the actual input field. Enumeration is key. 

### Injecting URLs
When dealing with [GET Request](../Concepts/Web/GET%20Request.md) and [POST Request](../Concepts/Web/POST%20Request.md) requests, you must match the `key:value` parameters of the URL and `[]` instead of `{}` is most circumstances. 

*For example:*
- `http://vulnsitecom/search?username=ben&role=user` &mdash; Normal URL NoSQL query
- `http://vulnsitecom/search?username[$ne]=bem&role=user` &mdash; Enumerating other users than "Ben"
- `http://vulnsitecom/search?username=admin&role[$ne]=user` &mdash; Finding a user `admin` that `does not` have the role `user`

A successful query will return as many values as match the injection. 
