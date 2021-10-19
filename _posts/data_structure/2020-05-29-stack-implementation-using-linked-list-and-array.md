---
layout: post
title: "Stack Implementations using Linked List and Array"
description: "Stack ADT Implementations using Linked List and Array data structures"
comments: true
keywords: "stack, linkedlist, array, list, data structures, adt"
---

The stacks are fundamental data structures. It has many usages from the language compiler, the back button in the web browsers to Undo in a word processor. The stacks use Last In First Out mechanism to insert/add and remove data from it. It can be implemented with either Linked List or Array. We will explore the implementation of stacks using both the data structures and their tradeoffs.

## Operations
The operation we require are:
1. `push()` - pushes an item onto the stack
2. `pop()` - removes an item from the stack
3. `isEmpty()` - checks if the stack is empty or not.

## Implementation using Linked List
The stack's implementation using Linked List is quite straight forward. We need to maintain a pointer to the first element of the linked list and we shall insert/remove the elements from the first element. We shall have an inner class Node that this model class/entity for an actual node/item. 
```java
private class Node  { 
      String item; 
      Node next; 
}   
```

The item is the actual data which is a String in this example. You can also have any other type of data that you want. The next variable is used to maintain the link to the next Node of the item. In the case of the last element, the next will always be null.

### Push
Pushing a new element/item will always be from the beginning of the list. For this, we need to save the first element temporarily into oldFirst. Since we are adding a new Node, we need to create a new node and assign it to the first element. The item to be inserted will also go in the item variable of the first. Finally, the previous first element that we save in oldFirst will be pointed by first.  
```java
public void push(String item) { 
      Node oldfirst = first; 
      first = new Node(); 
      first.item = item; 
      first.next = oldfirst; 
}
```

### Pop
Poping or removing an element/item from the stack is also from the beginning of the list. First, we save the item to be removed which will be returned at the last. The first node now points to the node which was its next node. The element/item is then returned.
```java
public String pop() { 
       String item = first.item; 
       first = first.next; 
       return item; 
}
```

## Implementation using Array
The arrays implementation uses an array S to store N items. We push items to the array at `S[N]` position and pop an item from `S[N-1]` position. We can handle the underflow of an array by throwing an exception when a pop operation is done on an empty array and overflow by resizing the array when we have crossed the size of the array. We can also add null items so that on the pop operation we can free the space.

### Strategies to Grow and Shrink the Array
We can always ask the client who will be using the Stack API to provide the size which is not a good idea because a client should not be caring about all that. We can increase or decrease the size of the array on push and pop, but this will also be very expensive. Think of a scenario where we are doing push-pop-push-pop-push. Here the strategy of increase or decrease the size by 1 will be very expensive. Hence we need to ensure that the array resizing happens as infrequent as possible.
1. When the array becomes full, we can create an array double the size of the array and copy all the items to it. 
2. Similarly, we can also halve the size of the array when it is quarter full. 
The question obviously will be why not halve the size of an array when it is half full, why quarter full? Consider the same scenario above of push-pop-push-pop-push ... when the array is full and each operation takes time proportional to N which can be too expensive.

![Array](https://github.com/sanjeevpr/sanjeevpr.github.io/blob/main/assets/images/Algo.png)

### Resizing
We can create an array of size 1.
```java
public Stack() { 
    s = new String[1]; 
}
```

For, resizing the array we shall have a method which does what we have discussed above:
```java
private void resize(int capacity) { 
       String[] copy = new String[capacity]; 
       for (int i = 0; i < N; i++) 
             copy[i] = s[i]; 
       s = copy; 
}
```

### Push
When the size of the array is full, we will resize the array to twice its size and add the array in Nth position. 
```java
public void push(String item) { 
          if (N == s.length) 
               resize(2 * s.length); 
          s[N++] = item; 
}
```

### Pop
We pop the item from the N-1 position of the array and resize the array to half if the size is 1/4th or quarter of the array size. 
```java
public String pop() { 
         String item = s[--N]; 
         s[N] = null; 
         if (N > 0 && N == s.length/4) 
              resize(s.length/2); 
         return item; 
}
```

### Tradeoffs between both the approaches
In the linked list implementation, every operation takes constant time in the worst case. It uses extra time and space to deal with the links between the nodes. While in cases of the array implementation, it takes around constant amortized time and there is also less wasted space. So you can choose whichever you like.

### Code
1. [https://github.com/sanjeevpr/data-structures/blob/main/Stack/ArrayStack.java](https://github.com/sanjeevpr/data-structures/blob/main/Stack/ArrayStack.java)
2. [https://github.com/sanjeevpr/data-structures/blob/main/Stack/LinkedListStack.java](https://github.com/sanjeevpr/data-structures/blob/main/Stack/LinkedListStack.java)