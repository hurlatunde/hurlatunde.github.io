---
layout: post
title: Firebase database for SQL developers - Part 2
excerpt: "Converting your SQL database structure to a non-schema / JSON database like Firebase"
description: "Converting your SQL database structure to a non-schema / JSON database like Firebase"
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
tags: Firebase Database SQL
---

#### Converting your SQL database structure to a non-schema / JSON database like Firebase

I, :) welcome to the second part for my posts on Firebase database for SQL developers 

[Firebase database for SQL developers - Part 1](https://hurlatunde.github.io/firebase-database-for-sql-developers)

In this post am going to take a relational model that we can see in a SQL database and then convert that to a No-SQL database like the Firebase database

![SQL](assets/images/post/relational.png)

the image above shows an events table, speakers table and event_speakers table. event_speakers is the table that relates events table to speakers tables together with something called [FOREIGN KEY](https://www.w3schools.com/sql/sql_foreignkey.asp "FOREIGN KEY" target="_blank")

To retrieve data from the SQL database image above the query will go as follow

![SQL](assets/images/post/selected.png)

So to what we have been waiting for translating the relationship in a Firebase database type

With the Event structur in mind we will want to create a JSON like database for the reslatioship

{% highlight json %}
{
  "Events": {
    "event_one": {
      "event_name": "Global event",
      "event_location": "Lagos Ikeja",
      "event_created": 16082017,
      "event_active": "active",
      "Speakers": {
        "0": "speaker_one",
        "1": "speaker_two",
        "2": "speaker_three"
      }
    },
    "event_two": {
      "event_name": "Developerlearn  friday session",
      "event_location": "Iwaya Sabo . Yaba",
      "event_created": 16082017,
      "event_active": "active",
      "Speakers": {
        "0": "speaker_one",
        "1": "speaker_two"
      }
    }
  },
  "Speakers": {
    "speaker_one": {
      "speaker_name": "Olatunde Owokoniran",
      "speaker_email": "hurlatunde@gmail.com",
      "event_created": 16082017
    },
    "speaker_two": {
      "speaker_name": "Femi Taiwo",
      "speaker_email": "dftaiwo@gmail.com",
      "event_created": 20082017
    },
    "speaker_three": {
      "speaker_name": "Mclord Adeola",
      "speaker_email": "mclord@gmail.com",
      "event_created": 22082017
    }
  }
}
{% endhighlight %}