---
layout: post
title: "Refactoring: A quick guide"
description: "A concise guide on refactoring"
comments: true
keywords: "refactoring, code"
---

## What?
- Systematic way of improving the code without adding new features.
- Not modifying the external behaviour
- Transforms mess of a code into clean code with simple design
- It can be a series of small changes, as the probability of mistakes is less.

## Why?
- Make the code cleaner, simpler and reduce complexity
- Easy to find RC of any bug
- Easy to add any new functionality or make any further changes
- Easier to test the code
- Easier to maintain the code
- We gain an indepth understanding of code
- Reduces tech debts
- More readable and hence becomes self-documenting

## When?
- While adding a feature
- While fixing a bug
- While code review

## How?
- TDD: Test - Implement - Refactor - Repeat
- Should be done as part of the development (feature addition/bug fixing/code review).
- Should be done in smaller chunks, each making the existing code better
- Should not add new feature or introduce a bug
- Should pass all the tests

## A Few Techniques
1. Composing Methods
- How to write/compose methods
- Extract methods- Grouping similar code
- Remove assignment from parameter - Use local variables instead of parameters
- Inline Methods - Calling a one liner returning boolean - Method can be removed

2. Moving features between classes
- Move functionalities b/w classes, create new classes
- Move method - Method is used more in the other class then in its own class - Move the method to its own class - Makes classes internally coherant/eliminate dependency on other class
- Extract Class - Does multiple things - Make two classes

## References
[https://refactoring.guru/refactoring](https://refactoring.guru/refactoring)
[https://martinfowler.com/books/refactoring.html](https://martinfowler.com/books/refactoring.html)
