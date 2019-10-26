---
layout: post
title:      "Rails Project - Beach Review App"
date:       2019-10-26 02:01:33 +0000
permalink:  rails_project_-_beach_review_app
---


For the Rails Final Project, we were tasked with building a Content Management System that manages data through complex forms and RESTful routes. I decided to expand upon my Sinatra project and create an elevated Beach Review App using the new functionality I learned in Rails.

As a new resident of Hawaii, I'm always looking for new beaches to explore around the island. However, I've noticed that there's so much unknown when looking at Google Maps, such as if the beach is too rocky to swim or if there are waves suitable for surfing (it's a hard life, I know). I created this app to take some of the guesswork out of visiting a new beach. 

This app allows users to write reviews for different beaches they visit in Oahu. They must enter an overall rating and description with the option to upload a photo, rate parking and surfing conditions, as well as select popular activities at that beach. They can edit and delete reviews they created as well as view reviews others have created.

The app has 3 models: user, review, and beach. A user has many beaches through reviews, a beach has many users through reviews, and a review belongs to a user and a beach. I incorporated a nested form within the review form, so a user could create a new beach if it didn't already exist. I added several validations to ensure the quality of the data before it saves to the database. I also added nested routes to allow users to create and view reviews from the beach show page.

To create the sign up and login features, I used the bcrypt gem to allow secure password storage in my database and utilized omniauth to allow users to login via Google. I love being able to sign up for different apps using my Google account, so I'm extremely happy that we learned how to implement this feature.

I spent a good amount of time refactoring and ensuring my app is DRY by creating additional helper methods and partials to follow Rails best practices.

My final step for this project was to add basic styling to make the app look a little more user-friendly. I hope to add more styling in the future.

Overall, I found this project very interesting and love how the concepts are building on one another. It was a very smooth transition from Sinatra to Rails and I'm looking forward to incorporating JavaScript in the future! 

Mood now that my Rails project is (hopefully) complete: 
![](https://imgur.com/9vF9Vm3)
Endangered Hawaiian Monk Seal passed out in front of a beautiful sunset at my local beach
