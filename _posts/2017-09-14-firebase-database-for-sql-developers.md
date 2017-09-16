---
layout: post
title: Firebase database for SQL developers - Part 1
description: "Understanding JSON / NoSQL database for SQL database"
excerpt: "Understanding JSON / NoSQL database for SQL database"
date:   2017-09-14 03:18:00
subclass: 'post tag-test tag-content'
navigation: True
logo: 'assets/images/hurla_logo_white.svg'
cover: 'assets/images/firebase.png'
comments: true
image:
  feature: firebase
  credit: Google Firebase
categories: [Firebase, SQL]
=tags: Firebase Database SQL
---


Most SQL developers are like "I would like to know if it is possible to use Firebase as a SQL database. I have trouble with relations in NoSQL."

It is not possible to use Firebase in this way. Firebase is a real-time object store. It is not a SQL database and is not intended to be a replacement for one. It completely lacks mechanisms such as JOINs, WHERE query filters, foreign keys, and other tools relational databases all provide. That doesn't mean it isn't a valuable tool. But any attempt to treat it "like" a SQL replacement is going to fail. That's not its purpose. But however it can give you the same end product as what you can achieve on an SQL database.

#### Firebase is a document-oriented / NoSQL database,

So am going to to go over how data is been stored better in sql databases and NoSQL database like the Firebase databases 

Relational databases use tables to store data, and a table is made up of columns in rows, and a column is a field of data like name, birthday or age, while a row is the entire record that represent 

![SQL](assets/images/post/sql.png)

To prevent null or empty input in the database row we use schemas.

#### A schemas is like a blueprints that tells the system how the data should be organized, it specified what the data-type is and also if it's required. this is called "constraints"

![SQL](assets/images/post/constraints.png)

one of the most important/special constraints is the primary key each row have them and must be unique because its use to uniquely identify each record.

If you want to insert data into this field that does not already exist in the database schemas for example inserting an extra field called **published** with the value of **TRUE**, Well it’s not going to allow that 

![SQL](assets/images/post/insert.png)

![SQL](assets/images/post/insert_error.png)

So to make that possible, one have to write an alter statement to add it to the schemas, This statement will have a **published** column and also a constraints

![SQL](assets/images/post/al.png)

![SQL](assets/images/post/altar.png)

But with NoSQL JSON databases like the Firebase database you don’t need any of the schemas and constraints mentioned above. **JSON is really simple it has keys, and values**. The key stands for an identifier while the value is just a value.

This provide a lot of flexibility so you don't go ahead and alter your schema just to updating a field that is not there 

However, just because it does not use schema and constraints does not mean you don't have to validate the data been saved to the firebase database. The Firebase database has a rules language called security rules

This rules allow you to specify the shape and size of data values before they get saved into the database, this way you still get to validate your data structure as if it was a schema with constraints

Keep in mind that the key use in any JSON like database is more like the identifier and as to be unique, It’s also the same thing as primary key in a SQL database 

#### More details on rules here: 
* [Firebase security](https://firebase.google.com/docs/database/security/)