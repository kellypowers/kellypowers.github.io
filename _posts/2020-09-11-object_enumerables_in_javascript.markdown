---
layout: post
title:      " Object Enumerables in Javascript"
date:       2020-09-11 18:28:00 +0000
permalink:  object_enumerables_in_javascript
---


For my Mock Technical Interview I was given a supplemental problem to practice with that included iterating over Objects.  I was stuck on this problem for some time, so I decided to do a dive into iterating over Objects in Javascript.


## for...in statement:
the terminology:
```
for (const prop in obj) { }

```
allows all properties of an object to be accessed.  

if we have 
```
const obj = {"key1": "value1", "key2": "value2}
```

using the for...in statement above means that prop will refer to the keys each iteration and obj[prop] will refer to the values.  

## Object.entries()
Object.entries()  returns an array of [key, value] pairs.  When used with for... of statement like the one below, you can refer to each of the object's keys and values.
```
for (let [key, value] of Object.entries(obj)) {
//block of code
}
```

The array returned would look something like [["key1", "value1"], ["key2", "value2"]]  but the order is not guaranteed.

## Object.keys() and Object.values()
As you would expect, Object.keys() returns an array of the keys of the object, and Object.values() returns an array of the values of the object passed into it.





