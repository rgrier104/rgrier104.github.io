---
layout: post
title:      "Asynchronous JavaScript"
date:       2020-04-25 22:36:08 +0000
permalink:  asynchronous_javascript
---


Today I want to take a deeper dive into synchronous and asynchronous JavaScript. Although JavaScript is naturally synchronous and people generally focus on synchronous execution as they’re learning to code, there are several techniques to allow for asynchronous code execution in order to make certain things, like running complex web pages, work more efficiently.

### Synchronous vs. Asynchronous JavaScript

Synchronous JavaScript runs lines of code one-by-one, meaning each line cannot be processed until the previous line has resolved. Running code synchronously works fine a lot of the time when processing simple tasks. However, you can imagine it’s not ideal when you have some sort of server request that takes some time to complete. You wouldn’t want your user to have to wait for that response in order for the rest of the code to process. These more time consuming requests would block everything else on a website, potentially causing users to leave your site/app out of frustration.

<iframe src="https://giphy.com/embed/26tk0Cmh8bdF9euAg" width="480" height="360" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/season-12-the-simpsons-12x6-26tk0Cmh8bdF9euAg">via GIPHY</a></p>

Asynchronous JavaScript removes the blocking aspect mentioned above. Additional code can continue to be processed while waiting for a response from server requests. For example, you can make a `GET` request to an API to get the current weather and then continue to update the DOM while waiting for the API response. Once you get the response, you can run additional functions and manipulate the data however you’d like. Asynchronous JavaScript allows your code to run more efficiently and can make the user experience a lot more pleasurable. 

#### Example: Synchronous code

```
let mollysBirthYear = 1950;
let billsBirthYear = 1945;
let currentYear = 2020;

console.log(`Molly is ${2020-1950} years old.`)

let billsAge = currentYear - billsBirthYear;
console.log(`Bill is ${billsAge} years old.`)

// Molly is 70 years old.
// Bill is 75 years old.
```
You can see everything appears to be running one after another.

#### Example: Asynchronous code

The global `fetch()` method available in most browsers is a common asynchronous function. I’ll take the fetch example from last week and add some `console.log`s to show the order in which code is processing. 

```
fetch("https://dog.ceo/api/breeds/image/random")
  .then(resp => resp.json())
  .then(data => {
    console.log(data)
    console.log(`Second`)
    })

  console.log(`First`)

// First
// {message: "https://images.dog.ceo/breeds/shiba/shiba-3i.jpg", status: "success"}
// Second
```
In this example, even though `First` is written *after* the fetch request, it is logged before the request response is returned! In this case, the first line of the fetch request, `fetch("https://dog.ceo/api/breeds/image/random")` runs and instantly returns a [*promise*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). I won’t go into promises too deeply in this post, but MDN defines a promise as: 
> an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value

So it’s basically just a placeholder while we are waiting for the actual response. We then move on to the next line of code (after all of the `.then` statements chained to the fetch): `console.log(“First”)`. Once the promise finally resolves with the actual response, the `.then` statements process and ‘Second’ is logged to the console.

I'll leave you with the adorable random dog photo that was returned by this API request. I love this [API](https://dog.ceo/dog-api/)!

![Imgur](https://i.imgur.com/TLpNgwG.png?1)

References:
* https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise




