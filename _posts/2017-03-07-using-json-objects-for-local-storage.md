---
layout: post
cover: 'assets/images/cover3.jpg'
title: Using JSON objects for local storage
excerpt: "Saving JSON object to browser local storage"
date:   2017-03-07 10:18:00
comments: true
tags:
    - Local Storage
subclass: 'post tag-test tag-content'
categories: 'casper'
categories: local_storage, Jquery]
navigation: True
logo: 'assets/images/hurla.svg'
---

When it comes to Local Storage i recommend using an abstraction library for many of the features discussed here as well as better compatibility.
* [jStorage](https://github.com/andris9/jStorage)
* [simpleStorage](https://github.com/ZaDarkSide/simpleStorage)
* [store.js](https://github.com/marcuswestin/store.js)

But sometimes i just love to use the best and easy approach, cos i think importing a library for something you may only use once or may end up not using up to 10% ability of the library.

### What is HTML Local Storage?
With local storage, web applications can store data locally within the user's browser.
Before HTML5, application data had to be stored in cookies, included in every server request. Local storage is more secure, and large amounts of data can be stored locally, without affecting website performance.
Unlike cookies, the storage limit is far larger (at least 5MB) and information is never transferred to the server.

Local storage is per origin (per domain and protocol). All pages, from one origin, can store and access the same data. [more info in w3schools](https://www.w3schools.com/html/html5_webstorage.asp)

#### SET local storage
{% highlight javascript %}
var userData = {name:'Olatunde Owokoniran', job-title:'Software developer'};
localStorage.setItem('user', JSON.stringify(userData));
{% endhighlight %}

#### GET local storage
{% highlight javascript %}
var localStorageData =JSON.parse(localStorage.getItem('user'));
console.log(localStorageData.name); //Olatunde Owokoniran
console.log(localStorageData.job-title); //Software developer
{% endhighlight %}

#### Iteration of all local storage keys and values
{% highlight javascript %}
for (var i = 0, len = localStorage.length; i < len; ++i) {
  console.log(localStorage.getItem(localStorage.key(i)));
}
{% endhighlight %}

#### DELETE local storage
{% highlight javascript %}
localStorage.removeItem('user');
delete window.localStorage["user"];
{% endhighlight %}

#### Read more:
* [html5_webstorage](https://www.w3schools.com/html/html5_webstorage.asp)
