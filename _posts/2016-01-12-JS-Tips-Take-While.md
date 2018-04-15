---
layout:     post
title:      How to implement TakeWhile in JavaScript
date:       2016-01-12
summary:    Implementation of C# Enumerable method TakeWhile in JavaScript.
categories: JavaScript
published:  true
---

In this post I will describe the ways how [TakeWhile](https://msdn.microsoft.com/ru-ru/library/bb548775(v=vs.110).aspx) method maight be inplemented in JavaScript. I will consider 3 implementations of this function and compare their performance. 

### Specification of function takeWhile.

Lets discribe syntax of function takeWhile we are going to implement.

#### Syntax

```js
takeWhile(source, predicate);
```

#### Parameters
- *source* - the sequence to return elements from
- *predicate* - a function to test each source element for a condition; invoked with arguments (element, index).

#### Description
As it is specified in [documentation](https://msdn.microsoft.com/ru-ru/library/bb548775(v=vs.110).aspx), function takeWhile should return elements from a sequence as long as a specified condition is true.

#### Example

{% gist Sufflavus/a450bc8a858658e7ee37 %}

### Implementation 1: Using *while*

{% gist Sufflavus/0bc96d22e7007bc4aff7 %}

In the first implementation I check each element of the *source* array while the *predicate* condition is true for the current element. When element is checked it is pushed in the result array.

### Implementation 2: Using *for*

{% gist Sufflavus/ab836bcbec1514994f8e %}

In the second implementation I go throw array and look for an index of the first element which does not fulfill the *predicate* condition. When index is found I call slice function to get the result array.

### Implementation 3: Using *some*

{% gist Sufflavus/3a0015453a127a20f578 %}

Here I use *some* to find the first element which does not fulfill the *predicate* condition. When index is found I call slice function to get the result array.

I found this one realization in the Internet. This one implementation seems to me pretty interesting and unusual so I desided to consider it as well.

### Performance

For tests I used an array of integers and a simple predicate:

{% gist Sufflavus/c4b34d7f4bd524cfc773 %}

Here is a result of performance [tests](http://jsperf.com/takewhile/2):

![performance](/images/posts/take-while-performance.png)

As we can see the fastest implementation is the first one. The performance is kinda different and depend on browser.

If you find any mistakes or have any suggestions please feel free to let me know. Thanks.
