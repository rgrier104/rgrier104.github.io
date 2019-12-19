---
layout: post
title:      "A Closer Look into JavaScript Scope"
date:       2019-12-19 20:19:11 +0000
permalink:  a_closer_look_into_javascript_scope
---


As I move through the React and Redux coursework, I am happy to see the added structure and organization. However, before I go any further in these libraries, I want to revisit a core concept that tripped me up a bit during my Rails/JS project: scope.

Scope is the current context of execution as defined by MDN Web Docs. It is the context where values and expressions are available for reference. Scope chain refers to all of the scopes available, from the local scope all the way to the global scope, including any outer scopes in-between. Basically, if a variable or function is not in the current scope or scope chain then it cannot be used. Inner/child scopes have access to outer/parent scopes, but not vice versa.

There’s also the concept of lexical scoping to throw into the mix - the scope that’s defined by *where* the variables or expressions are defined in the code. The scope is defined during the lexing phase, the first code compilation phase JavaScript performs. A function or variable will *only* have access to its scope chain where it is declared, which is very important when referencing functions inside other functions or using variables in multiple places throughout the code.

### Variable Declarations: Var, Let, Const & Scope

To complicate matters, the three variable declarations do not behave the same way when it comes to scope. `Let` and `const` have block scope whereas `var` has function scope. This essentially means that `var` is accessible anywhere in the function where it is declared, but` let` and `const` are only accessible in the block in which they are declared.

Here are some examples to better explain: 

```
function example1() {
 let i = 5;
 for (let i = 0; i < 3; i++) {
   console.log(i)
 }
 console.log(i);
}

example1()

// => 0
// => 1
// => 2
// => 5


function example2() {
 var i = 5;
 for (var i = 0; i < 3; i++) {
   console.log(i)
 }
 console.log(i);
}

example2()

// => 0
// => 1
// => 2
// => 3

```

In example1, `i` inside the for loop has a different scope than the `i` declared in the outer function when declared using `let`! In example 2, `i` has the same scope in the for loop and outer function when delcared with `var`. This definitely helps solidify why it is important to always use `let` and `const` vs `var`. 

