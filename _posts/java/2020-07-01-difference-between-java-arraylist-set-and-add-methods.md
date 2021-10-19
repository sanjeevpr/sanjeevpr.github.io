---
layout: post
title: "Difference between Java's ArrayList set and add Methods"
description: "Difference between Java's ArrayList set and add Methods"
comments: true
keywords: "java, linkedlist, array, list, data structures, adt, add, set, method"
---

There are many methods in the `java.util.ArrayList` class in Java. But, two of the overloaded methods `set` and `add` at index, are quite interesting. I am writing this post just to tell you a small gotcha of the methods.



## ArrayList Class
The ArrayList as the name suggests is an array but with dynamic size. A static array needs to be declared and initialized with a fixed int size that cannot change. But we don't need to specify the size of the ArrayList and it can grow dynamically as we add elements to it.

### There a two add methods
1. #### add(E e)
This basically adds the element to the ArrayList. Since the ArrayList is dynamic, it automatically increases the size of the ArrayList by 1, and adds the new element to the index.
2. #### add(int index, E e)
This is a little confusing because it shifts all the elements after the element has been added to the specified index. Let's say, you have an ArrayList with elements `[1, 2, 3, 4]` and the size is 4. If you try to add a new element 10 to index 2 where we have element 3 already, it won't replace element 3 with 10, but rather it will add 10 at index 2, and shifts all the remaining elements from 3 onwards to the right of the ArrayList. So, the resulting Arraylist looks something like this:

`[1, 2, 10, 3, 4]` and the size becomes 5

3. #### set(int index, E e)
As the name suggests, the set replaces the existing element in the index with the element that you want to add. So, for the ArrayList `[1, 2, 3, 4]` with size 4 after `set(2, 10)` becomes
`[1, 2, 10, 4]` and the size remains 4

### References
1. [https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)