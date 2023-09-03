---
layout: post
title: "Code Smells"
description: "Code smells are subtle signs in your codebase that hint at potential problems.
Recognize and eliminate them to keep your code clean and maintainable."
comments: true
keywords: "refactoring, code smells, design"
---

### Introduction

“Code smells” are specific coding pattern or practices in software development that indicate
potential issues or areas for improvement in the codebase. They are not necessarily bugs or errors,
but they can make the code harder to maintain, understand, or extend.

### Common Code Smells

1. **Long Method**
   - *Example*: A function with hundreds of lines of code.
   - *Code smell*: Long methods are challenging to understand and maintain. They should be broken down into smaller, more manageable functions.
2. **Duplicate Code**
   - *Example*: Repeated code blocks with only minor variations.
   - *Code smell*: Duplicate code are harder to maintain as a change would need to be done in multiple places which could lead to inconsistency. We can move such method to a common place.
3. **Large Class**
   - *Example*: A class with many attributes and methods
   - *Code smell*: Large classes can indicate it has multiple responsibilities. It’s better to break it into multiple small classes with single responsibilities.
4. **Nested Loops**
   - *Example*: Multiple levels of nested loops
   - *Code smell*: Deeply nested loops can make code harder to read and may indicate a need to refactoring or optimisation.
5. **Magic Numbers**
   - *Example*: Using numeric constants directly in code without explanation.
   - *Code smell*: Magic numbers are not self-explanatory and should be replaced with named constants or variables with descriptive names.
6. **Feature Envy**
   - *Example*: A method in one class frequently accesses the data or methods of another class.
   - *Code smell*: This can indicate the method belongs to the other class, violating the principles of encapsulation.
7. **God Class**
   - *Example*: A class that does too much, and many methods and attributes.
   - *Code smell*: Such classes are difficult to maintain and understand. They should be divided into smaller, more focused classes.
8. **Inappropriate Intimacy**
   - *Example*: Two classes that are tightly coupled, accessing each other’s private data and methods excessively.
   - *Code smell*: Tight coupling reduces code flexibility and lead to unexpected consequences when making changes.
9. **Hard-Coded Strings**
   - *Example*: Using string literals directly in code.
   - *Code smell*: Hard-coded strings make code less maintainable and harder to translate. They should be replaced with constants  or extracted to configuration files.
10. **Lack of Comments/Documentation**
    - *Example*: Code lacks explanations or comments
    - *Code smell*: Inadequate documentations makes it difficult for others (or even yourself) to understand the code’s purpose and usage.

### References
- [https://refactoring.guru/refactoring/smells](https://refactoring.guru/refactoring/smells)
