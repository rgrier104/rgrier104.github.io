---
layout: post
title:      "What are APIs? A brief overview"
date:       2020-04-19 01:12:38 +0000
permalink:  what_are_apis_a_brief_overview
---


Before I get into this week’s blog post, I want to give a quick update on my current situation. Unfortunately, I had a little accident this week and dislocated my shoulder. I was casually running outside in my neighborhood (like I’ve been doing 3-5 times a week ever since I’ve moved to Hawaii) and I tripped on some uneven sidewalk and fell which sent my shoulder out of its socket and into a place it doesn’t belong. It’s pretty crazy how something so little can completely derail your life! 

<iframe src="https://giphy.com/embed/ofiR5h351IjCM" width="480" height="402" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/falling-elephant-ofiR5h351IjCM">via GIPHY</a></p>

While this was easily the most painful thing I’ve experienced in my life, I’m so grateful I was able to quickly get to an urgent care center. A very nice doctor was able to pop that sucker back into place and I was the happiest I’ve been in a very long time! 

* Good news: there doesn’t appear to be any fractures
* Bad news: I can barely move my left arm

Needless to say, I’m quickly realizing how much I took moving my left shoulder for granted! Putting on clothes, showering, and cooking now come with some added difficulties. All in all, I’m so grateful that this inury appears to be relatively mild and hope to heal quickly. However, given the circumstances, I haven’t had much time to dig into a new software development concept this week.  Therefore, I’m coming to you with a review of a very important concept: APIs.

### What is an API?

API stands for Application Programming Interface. According to the Oxford dictionary, an API is:

> A set of functions and procedures allowing the creation of applications that access the features or data of an operating system, application, or other service.

Essentially, APIs allow different systems to communicate with one another in an easy, uniform way without needing to know the details of the external system. I’m going to focus on Web APIs because they are the most common and what I have used in my projects.

### Why use APIs?

APIs make it easy to share and access data. As a user, the real question is: why not use APIs? They let you easily access 3rd party data that you can integrate into your apps! But why would a company want to provide their data for free? Mostly, it’s to increase the number of users and dependency on the company, as well as improve the overall reach of the brand. When a developer sets up an API integration, they are more reliant on the company which results in the company’s data/service/product to become more valuable. However, there are many cases in which a company wouldn’t want to openly share their data, so many companies have private APIs that can only be accessed internally as well as partner APIs that can only be accessed by specific partners who most likely pay for the services from that company.

Overall, APIs are a really easy way to get your app to the next level. You can find a great list of public APIs [here](https://github.com/public-apis/public-apis). You can access things like weather data from NOAA and restaurant information from Zomato. 

### REST APIs
REST is a very common architectural style used in creating web services, like APIs. It stands for REpresentational State Transfer and is a set of standards that make it easier for systems to communicate with each other. There are 6 guiding principles you should adhere to, which you can read about [here](https://restfulapi.net/). You’ll also hear about SOAP protocol as a way to standardize API communication, but REST has recently become more popular and is generally easier to implement. 

Using REST principes, a client makes a request to the server including:
* An HTTP verb/method that states what you are trying to do 


```
- GET: simply get the resource from the server

- POST: create a new resource in the server

- PUT: edit/update the resource in the server

- DELETE: delete the resource from the server
```

* A header that contains information about the data being sent and what data it can accept
* A path to a resource
* Optional data (i.e. if you are POSTing a new recipe to the server, this body would include information about that recipe)

The server would then send a response indicating whether or not the request was successful and any requested data.


### Example: Make a fetch request from a popular API


Let’s say we want to use the [Dog API](https://dog.ceo/dog-api/documentation/random) to get a random picture of a dog. Using JavaScript, we can use the [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) method to make a GET request request to the dog API endpoint and receive a response with a dog picture!

```
fetch("https://dog.ceo/api/breeds/image/random")
  .then(resp => resp.json())
  .then(data => console.log(data))
```
In this code, we don’t need to include `GET` because that is the default method for `fetch`. `fetch` returns a promise. Once the promise resolves, we take the JSON response and convert it to a JavaScript object. We then take that object and log it to the console. If you run this in your console, you get something like: 

```
{message: "https://images.dog.ceo/breeds/spaniel-brittany/n02101388_3280.jpg", status: "success"}
```

After following the URL, we get this adorable photo!

![Imgur](https://i.imgur.com/TFQpQxx.png)

#### Resources
* https://www.codecademy.com/articles/what-is-rest
* https://dev.to/decipherzonesoft/types-of-apis-what-are-apis-different-types-of-apis-3mjm
* https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/



