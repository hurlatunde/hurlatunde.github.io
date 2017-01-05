---
layout: post
title: Firebase Query method
excerpt: "A more human understanding of firebase equerys"
categories: [Firebase, Query]
comments: true
tags:
    - NoSQL databases
    - Firebase
---

I believe for you to try and read about firebase query method, you probably have an idea of what firebase does.
But if not just know that firebase database is a NoSQL json databases which is a fancy way of saying its just json object :).
read more - [Firebase](https://firebase.google.com/docs/)

### The first query method that you need, always, is an orderBy.

{% highlight javascript %}
orderByChild(‘child-name’) // Orders alphanumerically by any child key
orderByKey() // Orders by the key, usually the fancy “push” keys that I referenced earlier
orderByValue() // Only relevant if your nodes don’t have children. If your list is not nested, with only one value, not sub-nodes, you might need orderByValue()
orderByPriority() // Don’t use this. In fact, don’t use any of the old $priority stuff. Firebase still supports it, but orderByChild() has made it irrelevant.
{% endhighlight %}
<br>

### Next, you need to decide how many records you want and which direction you want to order.

{% highlight javascript %}
limitToFirst(N) // Starts with the oldest record and reads toward newer records
limitToLast(N) // Returns N results from the newest records on the list, but returns them in
 {% endhighlight %}
<br>
ascending order, because Firebase only sorts in ascending order. So if I have records 1...10 and I run a limitToLast(3), I’d get records 8, 9 and 10 in that order.

### Finally, decide which key you’d like to start or end at.

{% highlight javascript %}
startAt(<Key>) // The key at which to start reading
endAt(<Key>) // The key at which to stop reading
{% endhighlight %}

There is still alot of things that still need to come to play before having a successful firebase query 

#### Read more:
* [firebase.database.Query](https://firebase.google.com/docs/reference/js/firebase.database.Query)
