---
layout: post
title:  "Immutability of Objects returned from Mongoose Query"
date:   2015-10-24 14:43:01
categories: mongoose
---

Yesterday, when I was working on creating server and database tests with my colleague [Joyce Liu](http://liujoycec.github.io/), we discovered that objects returned from Mongoose queries are not plain Javascript objects. 

Consider this simple find query: 

{% highlight js %}
  User.findOne({firstName: 'Lain'}, function(err, userRecord) {
    // do things
  })
{% endhighlight %}

If the user exists, the userRecord object being returned from the query is a Mongoose model instance in the same format as a plain Javascript object:

{% highlight js %}
  {
    _id: 25,
    firstName: 'Lain',
    lastName: 'Jiang',
    favoriteWriter: 'Marquez'
  }
{% endhighlight %}

If I try to mutate this object directly in any way, I will find that it is unsuccessful. For example, if I try to do something like:

{% highlight js %}
  User.findOne({firstName: 'Lain'}, function(err, userRecord) {
    userRecord.favoriteWriter = 'Borges';
    console.log(userRecord.favoriteWriter);
  })
{% endhighlight %}

The item that is being logged will still be 'Marquez' instead of 'Borges'. 

If we ever want to operate on the object, there are a few ways: 
1): Make a deep copy of userRecord through `JSON.parse(JSON.stringify(userRecord))`. That way, a new copy of this object will be created in the memory and will have lost the immutability that's linked to a Mongoose model instance.
2): Use .lean() in the query along with .exec() for the callback: 
{% highlight js %}
  User.findOne({firstName: 'Lain'}).lean().exec(function(err, userRecord) {
    // userRecord now is a plain Javascript object, by default mutable.
  })
{% endhighlight %}
3): Use .toObject on the model instance: 
{% highlight js %}
  User.findOne({firstName: 'Lain'}, function(err, userRecord) {
    userRecord = userRecord.toObject();
    // userRecord now is a plain Javascript object, by default mutable.
  })
{% endhighlight %}

In addition, if my query returns an array of objects, the array itself is mutable, and all the objects will be by default immutable Mongoose model instances. 
If any of my query object has a property that points to an object:
{% highlight js %}
  {
    _id: 36,
    firstName: 'Mario',
    lastName: 'Mario',
    girlfriend: {name: 'Peach', title: 'Toadstool'}
  }
{% endhighlight %}
In this example, the object that belongs to the property 'girlfriend' is indeed a plain, mutable Javascript object even when its parent object is still an immutable Mongoose model instance. 
