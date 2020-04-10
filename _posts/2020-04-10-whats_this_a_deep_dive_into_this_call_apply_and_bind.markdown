---
layout: post
title:      "What's this? A deep dive into this, call, apply, and bind"
date:       2020-04-10 21:31:02 +0000
permalink:  whats_this_a_deep_dive_into_this_call_apply_and_bind
---


For this blog post, I wanted to revisit some JavaScript fundamental concepts: execution context, this, call, apply, and bind. I know these concepts commonly come up during interviews, so I thought it’d be a good idea to refresh my memory and go through some examples. 

<iframe src="https://giphy.com/embed/QL5CItwwF5xU4" width="480" height="259" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/music-video-hilary-duff-raining-QL5CItwwF5xU4">via GIPHY</a></p>

### Execution Context & `this`

<iframe src="https://giphy.com/embed/l41YiPInyvdI4n98A" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/new-girl-fox-comedy-new-girl-l41YiPInyvdI4n98A">via GIPHY</a></p>

According to the [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this), `this` is:
> A property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object and in strict mode can be any value.

Execution context is essentially the environment in which JavaScript code is executed. Context can be passed implicitly or explicitly. There are 3 execution contexts in JS: global, function, and eval. 
* Global: Context outside of any function. `this` is a property of the global object - `window` for browsers
* Function: Context created when a function is invoked. `this` refers to the object the function was called on (what is left of the ‘.’)
* Eval: Context inside an eval function. I couldn’t find much information on this one as it’s not used frequently, so I’ll focus on global and function.

### Implicitly Setting Context

#### Function Context

```
let friday = {
    day: "Friday",
    whatDayIsIt: function() {
        return `It's ${this.day}`
    }
}

friday.whatDayIsIt()
// returns: `It’s Friday`
```

In this very simple example, we are invoking the function `whatDayIsIt` on `friday` so `this` in the function refers to `friday`.

#### Global Context

Let’s modify the above example a bit:
```
let whatDayIsIt = function() {
        return `It's ${this.day}`
    }

whatDayIsIt()
// returns: `It’s undefined`
```

This time, `this.day` returns undefined because we are calling `whatDayIsIt` on the global object, `window`. `Window` doesn’t have a `day` property, so `this.day` is undefined. If you run:

```
let whatDayIsIt = function() {
        return this
    }
whatDayIsIt()
```
 `Window {parent: Window, opener: null…` is returned proving `this` is the global window object.

### Explicitly Setting Context using `call`, `apply`, and `bind`

#### `call` and `apply`

[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) provide the following definition:

> The `call()` allows for a function/method belonging to one object to be assigned and called for a different object. `call()` provides a new value of this to the function/method.

It accepts `thisArg` (what becomes `this`) and any additional arguments you want to pass to the function.

```
let friday = {
    day: "Friday",
}

let whatDayIsIt = function() {
        return `It's ${this.day}`
    }

whatDayIsIt.call(friday)
// returns: `It’s Friday`
```

Awesome, we can *call* `whatDayIsIt` on `friday` even though `friday` doesn’t have a `whatDayIsIt` method! `call()` changes `this` to `friday`.

Here’s an example where we call in additional arguments to the function:

```
let friday = {
    day: "Friday",
}

let whatDayIsIt = function(reaction) {
        return `It's ${this.day}. ${reaction}`
    }

let reaction = "YAY!"

whatDayIsIt.call(friday, reaction)
// returns: `It’s Friday. YAY!`
```


`apply` is very similar to `call` except you pass an array as the second argument. If the function needs several args, using `apply` with an array would be easier than typing out all individual arguments.

#### `bind`

[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) provide the following definition:

> The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

Essentially, this means that `bind` returns a function rather than invoking the function like `call`. 

```
let friday = {
    day: "Friday",
}

let whatDayIsIt = function(reaction) {
        return `It's ${this.day}. ${reaction}`
    }
 
let reaction = "YAY!"

let fridayFn = whatDayIsIt.bind(friday)

fridayFn(reaction)
// returns: `It's Friday. YAY!`
```

In this example, we are permanently setting `this` to `friday` and saving it as a function that can be called with different function arguments.

I hope this was helpful! I definitely feel more confident in my knowledge after playing around with these concepts in my console. Now time for the weekend! Can you tell I'm excited that it's Friday? 

References:
* https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/
* MDN Docs referenced above




