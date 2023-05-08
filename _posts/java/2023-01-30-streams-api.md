---
layout: post
title: "Streams API"
description: "An introduction to Java 8 Stream APIs"
comments: true
keywords: "java, stream, lambda, functional programming"
---
### What is Stream

- Stream is a sequence of elements supporting sequential and parallel aggregate operations.
- Streams bring functional programming to Java

### Advantages

- Easier and concise APIs
- Make heavy use of lambda which brings goodness of lambdas
- ParallelStreams makes it easy to do multi-threaded operations.

### Stream Pipeline

To perform computations, stream operations are composed into a stream pipeline.  A pipeline consists of

1. Source: is from where the data comes to the stream. Eg. collections, I/O channel, etc.
2. Zero or more intermediate operations
3. One terminal operation.

### Stream Source

A stream source can be array, collections, I/O channel. These usually have the method to create a stream.

### Stream Operations

The operations that are performed on the stream can of two types

1. **Intermediate**

   These operations return a stream so these can be chained together. Eg. map, filter, sort, etc.

   For large datasets, we should use ParallelStream to leverage multi-threading.

2. **Terminal**

   These operations either return a non-stream value or void. Eg. forEach, collect, reduce, etc.

   - forEach applies the same function to each element in the stream
   - collect is use to collect the elements to a collection (list, set, map)
   - reduce are specialise operations to count(), sum(), avg(), min(), max(), summaryStatistics() etc.

### Examples

```java
IntStream
    .range(1, 10)    // Creates a int stream from 1 to 9
    .forEach(System.out::println);
// Result
// Prints from 1 to 9

IntStream
    .range(1, 10)
    .skip(5)    // Skips the first 5 elements
    .forEach(i -> System.out.println(i));

// Result
// Prints from 6 to 9

int sum = IntStream
    .range(1, 5)
    .sum();

// Result
// sum is 10

Stream.of(2, 1, 3)
    .sorted()
    .findFirst()
    .ifPresent(System.out::println)

// Result
// 1

String names[] = {"Sanjiv", "Minu", "Hemu"};
```

### Reference
[https://www.youtube.com/watch?v=t1-YZ6bF-g0&ab_channel=JoeJames](https://www.youtube.com/watch?v=t1-YZ6bF-g0&ab_channel=JoeJames)
