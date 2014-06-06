Functional Javascript: The Good Parts
=====================================

Follow Along: [github.com/seanhess/angularjs-typescript](github.com/seanhess/angularjs-typescript)

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

Wait, What?

The alternative: Imperitive Programming
------------------------------------
Series of instructions to the computer to access & modify memory. 

```
// I understand (sort of) how every line translates into machine code!
var totalAge = 0
for (var i = 0; i < users.length; i++) {
    totalAge += users[i].age
}
```

Functional Programming
----------------------
Functions as high-level tools you combine to do something. Math!

```
// oh, so we're summing the array of ages, got it.
var totalAge = users.map(userAge).reduce(sum)
```

[History: a separate track:](http://en.wikipedia.org/wiki/Functional_programming#History)

- 1930 Lambda Calculus
- 1958 Lisp and friends, John McCarthy
- 1977 FP and composition. John Backus
- 1978 ML
- 1987 Haskell

Why functional programming?
---------------------------
*What* instead of *How*

Guarantees mean we can make nifty assumptions. Easier maintenance.

More code is reusable. Toolbox to Workshop

More expressive. Orders of magnitude smaller. 

Tradeoffs: Bigger Vocabulary
----------------------------

> Reduce? What is this new devilry? — Boromir

Failing to convince people at I.TV


Concepts: Pure Functions
-------------------------

> Elevate the pure functions from the impure, lest they drag your whole codebase into the mire. — Saint Curry (not the spice)

"Pure" functions return a result based only on what you pass in.

### Example: Isaac Netwon
```
class Apple {
    constructor(gravity) {
        this.y = 0
        this.gravity = -9.8
        this.velocity = 0
    }

    // fall depends on this.gravity, and this.y, which can change. 
    // this is the right equation, I think...
    fall(dt) {
        this.y += this.gravity * dt
    }
}
```

Separate out the pure calculation:

```
// look at this nice function I found on NPM!
// Wow my function was really buggy. 
function doPhysics(a, v0, dt) {
    return v0*dt + (a*dt^2)/2
}

var distance = doPhysics(apple.gravity, apple.velocity, dt)
apple.y += distance
```

### What's the point of pure?

- much easier to test
- more reusable. Independent of the object
- easier to refactor
- optimizations like memoization and concurrency
- do an independent calculation? 


Concepts: Higher Order Functions
--------------------------------

> "There's a function for that" — Haskell the Supreme Logician, in reference to pretty much your entire codebase

Higher Order Functions take a function as a parameter, or return a function. They let us reuse code in places we wouldn't expect, like loops.

### Example: I'm old so I know stuff

```
var bestProgrammer;
for (var i = 0; i < programmers.length; i++) {
    if (!bestProgrammer || programmers[i].age > bestProgrammer.age) {
        bestProgrammer = programmers[i]
    }
}
```

What is reusable about the above? Everything but `.age`.

```
function maximum(items, toValue) {
    var maxItem
    for (var i = 0; i < items.length; i++) {
        if (!maxItem || toValue(items[i]) > toValue(maxItem)) {
            maxItem = items[i]
        }
    }
    return maxItem
}
```

The above belongs in an NPM module, and is no longer a part of our code base. POOF!

```
bestProgrammer = maximum(programmers, function(person) {
    return person.age
})

// ES6 version
bestProgrammer = maximum(programmers, (person) => person.age) 
```

This is much easier to read. `Maximum` is most likely maintained by someone else in the community and becomes well-tested. We can forget about how it works. 

See [lodash.com](lodash.com) for many common higher order functions.

Concepts: Composition
---------------------

> "I like tiny programs that do one thing well and one thing only. Which hypothetical reusable modules would make the task at hand trivial?" — substack

Build very focused tools, then use them to do something bigger. Here's our `totalAge` code from before. 

```
// I understand how every line translates into machine code!
var totalAge = 0
for (var i = 0; i < users.length; i++) {
    totalAge += users[i].age
}
```

First we need some new tools. 

[`Array.map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) converts each item in an array to something else:

```
[1,2,3].map(function(n) { 
    return n*2 
})
// -> [2,4,6]
```

[`Array.reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) aggregates data from an array into a single value

```
[1,2,3].reduce(function(total, n) {
    return total + n
}, 0)
// -> 6
```

Let's make a `sum` function, which does the same thing as `+`. as well as a function that gives the users' age

```
function sum(a, b) { return a + b }
function getAge(object) { return object.age }
```

That's 4 new tools in our toolbox: `map`, `reduce`, `sum`, and `getAge`. With all 4 of these, our original code becomes trivial.

```
var totalAge = users.map(getAge).reduce(sum)
```

Our composed application code is very unlikely to be buggy. Any bugs are probably in the individual functions, most of which come from well-tested 3rd party libraries. 

Principles

- do one thing, do it well
- most basic parameter possible
- someone already wrote it

Composition-Driven Development
------------------------------

Start writing the application code as if the functions exist. Start with *What*. Go back and write the new tools you need later.

```
function solveWorldHunger(population) {

    // hmm, this seems hard, but if I break it down...

    var food = getSoylent(population * MUCHO)
    var shipping = efficientDistribution(food)
    var economy = fixWorldEconomy(Time.MaybeTomorrow)
    return combine(shipping, economy)
}
```

3rd party libraries: make your most important calculations available as focused functions! You can't anticipate everything!

A map through the wastes
-------------------------
Beware of excessive partial application. Just use lambdas.

```
[1,2,3].map((n) => sum(n, 2))  // more clear
[1,2,3].map(sum.bind(null, 2)) // not worth it
```

The `compose` function is not really worth the confusion. Just use lambdas.

```
function greet(name) {
    return "Hello ", + name
}

function excitedly(message) {
    return message+"!"
}

var welcome = _.compose(greet, excitedly)      // what is welcome?
var welcome = (name) => excitedly(greet(name)) // easier to understand
welcome("UtahJS")
```

Crazy recursive loops

```
function eatAndDisgest(array) {
    var item = array.pop()
    return item + eatAndDisgest(array) // the stack hates you
}
```

Use a type system! 

We all Win
----------

If we focus on composable code we can all build off each other's work. 

*What* instead of *How*. Smaller code bases. Refactoring. Maintenance

The END
==========

[github.com/seanhess/functional-javascript][talk]

Contact Me: [@seanhess][@seanhess]



[talk]: http://github.com/seanhess/functional-javascript
[@seanhess]: http://twitter.com/seanhess
