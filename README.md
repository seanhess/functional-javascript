Functional Javascript: The Good Parts
=====================================

> Functional programming encourages us to organize our code well and helps us create code that is easier to reason about. The less we reinvent the wheel and use a well-tested tool, the easier it is to maintain our application code. 

> "Pure" functions return a result based only on what you pass in. You never have to worry it is going to do something unexpected. Higher order functions (functions that take other functions as parameters) let us reuse code in places we wouldn't expect, like loops. Composition allows you to create larger tools from smaller ones. 

> Javascript is a great functional language, but some ideas are harder to implement than others, and some aren't worth using in JS at all! After having wandered the Functional JS wastes for a few years, I will tell you stories of the dangers that lurk, as well as the rewards that await you if you apply Functional JS wisely.

About Me
--------
Sean Hess

Programmer, Inventor, Startup Advisor. Solve hard problems, make productive workplaces. 

- Twitter: [@seanhess][@seanhess]
- Blog: [seanhess.github.io](http://seanhess.github.io)
- Github: [github.com/seanhess](http://github.com/seanhess/)


What is Functional Programming?
-------------------------------

> In computer science, functional programming is a programming paradigm, a style of building the structure and elements of computer programs, that treats computation as the evaluation of mathematical functions and avoids state and mutable data.
— Wikipedia

### Imperitive Programming
- series of instructions to the computer to access & modify memory. 
- Focus on HOW it works

```js
var totalAge = 0
for (var i = 0; i < users.length; i++) {
    totalAge += users[i].age
}
```

### Functional Programming
- Functions as high-level tools you combine to do something. 
- Focuses on WHAT it does

```javascript
var totalAge = users.map(age).reduce(sum)
```

Why functional programming?
---------------------------
    - what you want, instead of how
    - more expressive: less application code, more reusability, fewer points of failure, larger code bases
    - concurrency, other automatic optimizations
    - 
- downsides to functional programming
    - learning curve. unfamiliar.
- Functional Concepts
    - pure functions
    - higher order functions
    - composition

    - partial application?
- Pure Functions
    - memoization
- Higher Order Functions
- Composition
    - summing an array with reduce
    - var totalPoints = posts.map(postPoints).reduce(sum)
- What to avoid
    - partial application and composition
    - things like recursive loops
- Conclusion: The biggest wins
    - code size
    - refactoring
    - desigining code via 


The END
==========

[github.com/seanhess/functional-javascript][talk]

Concat Me: [@seanhess][@seanhess]






GOOD THINGS TO EMPHASIZE
- code size
- designing code one tool at a time
- 




NOTES
------

MAJOR CONCEPTS
- what is functional programming?
    - Imperitive: series of instructions to the computer to modify memory. Focus on HOW
    - functions are used everywhere, to read, transform, etc. 
- why functional programming?
    - more expressive (less code), safer, some features that are impossible in normal languages
    - what you want, instead of how
    - think in terms of reusability
    - orders of magnitude less code. 
        - Fewer points of failure.
        - can handle larger code bases
    - concurrency
- pure function
    - no side effects
    - automatically concurrent-friendly. Can't have data races!
    - easier to understand what it does
- higher order functions
- composition
    - smaller, focused functions
- things to avoid
    - too far down the composition and currying rabbit hole
- biggest wins
    - refactoring
    - building an app a piece at a time
    - reusable pieces

- things Javascript can't do
    - haskell can fuse multiple loops into one.
    - automatic event-loop
    - automatic parallelization

- minimize complexity

- *requires more skill, bigger learning curve.  
    - easier to understand every line != better program



[talk]: http://github.com/seanhess/functional-javascript
[@seanhess]: http://twitter.com/seanhess
