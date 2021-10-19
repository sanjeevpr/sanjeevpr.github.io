---
layout: post
title: "var versus let Keyword"
description: "var versus let Keyword in JavaScript"
comments: true
keywords: "var, let, javaScript"
---

The `var` and `let` keyword can get very confusing and may lead to unexpected behaviors in an application and may also lead to some silly bugs. I will explain what is both and when to use one.

Take a look at the code below,
```javascript
function do() {
 for(var i = 0; i < 5; i++) {
 console.log(i);
 }
 console.log("Final value of i : " + i);
}

do();
```

What is the expected output? I know, you might well say this code prints undefined in the last line. I also thought so. But no. The output of the following code is:

```javascript
0 
1 
2
3
4
Final value of i : 5
```
  
There is a simple explanation for it. A variable declared with the `var` keyword is accessible to the whole function in which it is declared rather than just the block. In the code above, although the variable i is declared inside the for loop, it is available outside it also as the for loop itself is inside the function do(). This is called variable hoisting in JS. In other programming languages such as Java or C++ etc, this code will throw a compile-time error immediately. We need to be very careful with the usage of the `var` keyword.

The code is written with `let` keyword,
```javascript
function do() {
 for(let i = 0; i < 5; i++) {
 console.log(i);
 }
 console.log("Final value of i" + i);
}

do();
```

While the variable `i` declared with the `let` keyword behaves properly in the case above. It will throw an error in 
`console.log("Final value of i" + i);`
line if we compile this code with TypeScript.

My thoughts with the usage of both should be known first. We should use the `let` keyword in most of our variable declarations. The `var` keyword can be used in the scenarios where you want the variable to access inside the whole function.
