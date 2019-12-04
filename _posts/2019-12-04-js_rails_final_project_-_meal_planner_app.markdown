---
layout: post
title:      "JS/Rails Final Project - Meal Planner App"
date:       2019-12-04 20:39:27 +0000
permalink:  js_rails_final_project_-_meal_planner_app
---

For my JavaScript & Rails final project, I created a meal planner single page application that allows users to plan out their meals for a given week. Recently, I switched over to a whole foods, plant based diet for my health, the environment, and the well being of the animals. However, I have found it pretty challenging to efficiently plan out healthy meals for my boyfriend (who eats enough for 3 adults) and me every week. I would find myself looking through blog after blog for hours, but never piecing together a cohesive weekly meal plan. I would write down ingredients and then forget what meal they were for and what blog housed the recipe. This inspired my idea to create a meal planning application for my final project. My app allows you to add recipes you like to the database along with the link to the corresponding blog recipe. You can then plan out your weekly meals by adding a recipe from the database to each day, so the recipe and URL are right there whenever you need them. There is also a notes section where you can write down any ingredients you might need or information on what items need to be prepped ahead of time. In the future, I’d like to add models for the ingredients and measurements for each recipe, but it was a bit too time consuming for this project.

The project has a Rails backend and JavaScript, CSS, and HTML frontend, which was a really great learning experience for me. I came into this project feeling very unprepared compared to how I felt before starting the past projects. I took everything one step at a time and built out each feature vertically and am really impressed with what I was able to create. 

The app has 3 models: recipe, meal plan, and meal. I struggled with figuring out the best way to store the information considering there are up to 28 recipes and 7 days for each meal plan, but decided to structure the app with a join table, meals, that connects the recipes and meal plans.  The app also uses several fetch requests to communicate with the server in order to create and update meal plans, create meals, and create, read, and delete recipes. The majority of the UI on the app is added using JavaScript, which was a great way for me to really understand how JS can manipulate the DOM. I was able to create functions that would add the meal plan calendar without having to rewrite the same code for each meal and day.

I have a lot of additional features I’d like to add to the app, but decided to save most of them for the future in the interest of moving along in the curriculum. In the future, I’d love to add ingredients, filters and search functionality, as well as the ability to view and reuse old meal plans. I know it will be fairly complex to recreate an old meal plan in the calendar display, but I think that will be a great addition to the 2.0 version down the road.

Although this project was pretty difficult and daunting, I’ve learned so much and have definitely elevated my JS knowledge to the next level. I’m proud of what I created and am really looking forward to coming back to make improvements in the future.

