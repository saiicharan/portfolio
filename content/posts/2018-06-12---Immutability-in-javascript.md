---
title: Immutability in JavaScript
date: "2018-06-12T00:46:37.121Z"
template: "post"
draft: false
slug: "immutability-in-javascript"
category: "Tech"
tags:
  - "Tech"
  - "Javascript"
description: "Immutability in JavaScript explained with examples"
socialImage: "/media/mutate.gif"
---

> It’s a mutation. It’s a very groovy mutation. I’ve got news for you, Amy. You are a mutant. — Professor X

![A still from the movie](/media/mutate.gif)
*Source: https://www.reddit.com/r/PixelArt/comments/60exmj/ocwip_goku_super_saiyan_transformation/*

Before I address the topic of Immutability, lets actually find out what mutation is.

### Mutation
Anything that changes/transforms the behavior or the structure of an object is called mutation. Like the force mutating Goku in the above picture.

### Mutation in JavaScript
The definition might seem pretty similar to the above example. Although, in JavaScript, it looks something like this,

![Basic Mutation](/media/basic-mutation.png)

### But, Why is mutation a problem in JavaScript?
Before I answer this question, let me talk about a few concepts about Pass by Value and Pass by Reference in JavaScript.

### Pass by Value
Consider the following example,

![Pass By Value](/media/pass-by-value.png)

In the above example, I create a variable "a" with a value of 5 and assign it to a variable called "b". Then, the value of "a" as well as "b" would be 5. In this case, I have **passed the value** of "a" to "b".

Now let’s say I change the value of "a" to 15. In doing so, my "b" value does not get changed because it was passing initially by a **value**. This way of passing the **values** of variables to another variable can be stated as **pass by value**.

### Pass by Reference
Consider the following example,

![Pass By Reference](/media/pass-by-reference.png)

In the above example, I create an object and assign it to the variable “object1”. I create another variable “object2” and assign “object1” to it.

Now in line number 7, I mutate “object1”’s name property to “charan”. Surprisingly, when I log the value of “object2” the name property of “object2” has also changed to “charan”. So what exactly happened here? Objects are usually **passed by reference**. Since object2 is equated to object1, it is **passed by reference**, meaning, they both hold the same memory location. So, when we change the value of object1, object2 usually gets changed.

![Memory](/media/memory.png)
*Both object1 and object2 point to the same memory location*

We can find a similar problem in case of arrays as well. Consider the below example,

![Pass By Reference Array](/media/pass-by-reference-array.png)

Both arrays and objects are **passed by reference**.

How is this a problem? Imagine, you pass an object/array across various functions, and you mutate it at some point, the same object/array might be mutated in other places, leading to unexpected behavior in some parts of the code, resulting in bugs.

### Solution: Going Immutable!

One way of achieving immutability in JavaScript is by using 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign" target="_blank">Object.assign</a>

![Object Assign](/media/object-assign.png)

In the above example, we are using Object.assign to create “object2” variable. Object.assign usually takes in three values, an initial value, the source object and the replacing object. In our case the initial value is an empty object, we get the contents of “object1”, and to that we add a new object {name: ‘charan’}. If there is already a property ‘name’ in object1, it gets replaced with the existing value(in our case, ‘charan’) and assigns it to the initial value(which is an empty object). So now, my object2 is a fresh object. The mutations of “object1” do not affect object2, since now both refer to different memory locations.

Another way to achieve immutability in JavaScript is by using the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax" target="_blank">spread operator</a>.

![Spread Operator Object](/media/spread-operator-object.png)

The above example does the same thing as Object.assign, but the syntax looks a lot cleaner.

In arrays, immutability can be achieved by using the same spread operator.

![Spread Operator Array](/media/spread-operator-array.png)

In the above example, 6 gets added to the “newArr” variable. The mutations of “arr”, as in the line number 7, does not affect “newArr” variable. Also, for arrays in JavaScript, <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map" target="_blank">map</a>,
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter" target="_blank">filter</a>,
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce" target="_blank">reduce</a>
can be used to avoid mutations since they return new arrays every-time they are called.

Writing **immutable Javascript** code is a good practice. I hope this article gives you a basic idea of how variables are stored in memory and how immutability helps you write better quality code. Feedback and suggestions are welcome. :)

