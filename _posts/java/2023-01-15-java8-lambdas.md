---
layout: post
title: "Java 8 Lambdas Basics"
description: "An introduction to Java 8 Lambdas and Stream APIs"
comments: true
keywords: "java, lambda, stream, functional programming"
---

## Why Lambdas
1. Enables functional programming
2. Readable and concise code
3. Enables parallel programming
4. Easier to write and use libraries written in Lambdas, etc

## What is functional programming
It is a way of writing code where only pure functions and immutable values are used.

1. Pure Functions
    - The output of the pure functions depend on the input of the functions.
    - It has no side-effects meaning it does not read or write anything from the outside world.
    - As a result, if you call a pure function infinite times with input x, it will always return y.
2. Immutable
    - The values passed to a function cannot be re-assigned or changed. This is very important for concurrency.

From Java 8, we use a mix of both OOP and FP.

### Why do we need FP in Java
Imagine that we want to write a small function/method. For that, we would need to write a class containing the method. The method cannot stay in isolation. This is what FP is all about. We can now create a method in isolation. We do it using lambdas.

Example:

```java
public class Greeter {
	public void greeter() {
		System.out.println("Hello world!");
	}
}
```

Now this can be created using lambdas without having to create a Greeter class.

```java
greet = () -> System.out.println("Hello world!");
```

We have removed the things that are not required from the method like public, the name of the method, and the return type as the complier is smart enough to figure that out.

The variable greet now contains a block of code (function) as its value. The greet variable can be passed around and assigned to other variable as if it is a value like string or number.

Few more examples

```java
sum = (int a, int b) -> a + b;
safeDivide = (int a, int b) -> {
    if(b == 0) {
        return 0;
    }
    return a / b;
};
```

## Type of the Lambda functions
1. We had not declared the type of the lambda function variable in the above example.
2. To do so, we need to create an **interface** with **only a single abstract method** with the **same signature as the target lambda expression/function**.

```java
MyGreet greet = () -> System.out.println("Hello world!");

MySum sum = (int a, int b) -> a + b;
...
...
}

interface MyGreet {
    void greet();
}

interface MySum {
    int sum(int a, int b);
]
```

The signature has to match the lambdas. Since, the greet function does not return anything, the return type becomes void.

### Lambdas vs Interface

```java
class MyGreet implements Greet {
    void greet() {
        System.out.println("Hello world!");
    }
}

interface Greet {
    void greet();
}

main () {
    Greet greetInstance = new MyGreet();    //1
    greetInstance.greet();
    
    Greet greetLambda = () -> System.out.println("Hello world!");  //2
    greetLambda.greet();

    Greet greetInner = new MyGreet(        //3
        @Override
        void greet() {
            System.out.println("Hello world!");
        }
    );
}
```

Line 1 is an instance of class Greet which has an implement of the greet method in MyGreet class.

Line 2 is the just a function which is implementing the method in the interface Greet. It is not implementing the class. It is almost similar as the anonymous inner class in line 3.

### Type Inference

```java
main() {
    
    Greet greetLambda = (String s) -> s.length();    //1

    Greet greetLambda = s -> s.length();    //2
    printLength(greetLambda);
    printLength(s -> s.length());    // Inlined
    
    public static void printLength(Greet greetLambda) {
        int length = greetLambda.getLength("Hello");
        System.out.println(length);
    }
}

interface Greet {
    void getLength(String s);
}
```

### Backward-compatibility

The lambdas were not implemented as new type but rather reuse the interface construct that Java has because introducing new type to already existing libraries would break the old code using the libraries.

Example: This is how we can use lambdas with the existing classes like Thread without breaking it.

```java
// We are able to pass a lambdas (like an instance of Runnable) because the Runnable is an interface and has just one abstract method in it.

Thread myThread = new Thread(() -> System.out.println("Hello from lambda"));

interface Runnable {
    public void run();
}
```

### Functional Interface

- The interface that use to create lambdas are called Functional Interface.
- The Functional Interface always has just one abstract method.
- It may have default methods (concrete) from Java 8.
- It is a good practice to mark the functional interface with @FunctionalInterface, but this is optional.

Java provides a package [java.util.function](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) for most of the common methods that the developer might use. This was created so that the developer don't need to rewrite a functional interface for common kinds of  methods.

Example:

Java has functional interface Consumer<T> has a abstract method which takes in one argument of generic type T and doesn't return anything.

So, if we have such a requirement and instead of rewriting everything, we can leverage this interface.

```java
String name = "Sanjiv";
printName(name, name -> System.out.println(name));

public static void printName(String name, MyPrinter printer) {
    printer.print(name);
}

@FunctionalInterface
interface MyPrinter {
    void print(String s);
}

// Instead of writing out own functional interface, we can use the Consumer functional interface form java.util.function package

public static void printName(String name, Consumer<String> printer) {
    printer.accept(name);    // Does the passed behaviour
}
```

There are other methods in the different interfaces like BiPredicate, which takes two arguments and returns a boolean.

```java
String personOneName = "Sanjiv";
String personTwoName = "Minu";

boolean isBigger = compareNames(personOneName, personTwoName, (p1, p2) -> p1.compareTo(p2));

static boolean compareNames(personOneName, personTwoName, BiPredicate<String, String> biPredicate) {
    return biPredicate.test(personOneName, personTwoName);
}
```


### Exception Handling in Lambdas

```java
static void arithmeticOp(int first, int second, BiComsumer<Integer, 
Integer> consumer) {
    consumer.apply(first, second);
}

arithmeticOp(1, 0, (first, second) -> {
    try {
        System.out.println(first / second);
    } catch (ArithmeticException e) {
        System.out.println("Number divided by zero");
    }
});

// This way of doing the exception handling is not very elegent and 
// results in a bigger code

// Here we will use a wrapper function which just handles the exception

private BiComsumer<Integer, Integer> consumer wrapperLambda(
BiComsumer<Integer, Integer> consumer) {
    return (first, second) -> {
        try {
            consumer.accept(first, second);
        } catch (ArithmeticException e) {
            System.out.println("Number divided by zero");
        }
    };
}

// This is how we call the wrapper instead of calling the main wrapper
arithmeticOp(1, 0, wrapperLambda((first, second) -> 
       System.out.println(first / second);
));
```

In the example, we have wrapper out main lambda with a wrapper lambda which does the same thing with addition to handling exception.

There are actually other ways to handle exception.

### this Reference

The lambda doesn't override or get a new "this" object inside the block. It points to the "this" which is outside the lambda

```java
class Example {
    public void doProcess(int i, Consumer<Integer> consumer) {
        consumer.accept(i);
    }

    main() {
        Example example = new Example();
        example.doProcess(10, i -> {
            System.out.println(i); 
            System.out.println(this);
        });

    }
}
// this in the above example still points to the Example class instance. Lambdas doesn't get a new object.
```

### References
1. [https://www.youtube.com/watch?v=4mmOTCIZI1M&list=PLqq-6Pq4lTTa9YGfyhyW2CqdtW9RtY-I3&index=3&ab_channel=JavaBrains](JavaBrains YouTube Channel)
2. [https://alvinalexander.com/scala/fp-book/what-is-functional-programming/](alvinalexander.com)
