---
layout: post
title:      "Sinatra Project: Oahu Beach Review App"
date:       2019-09-18 18:26:56 +0000
permalink:  sinatra_project_oahu_beach_review_app
---


Aloha from Hawaii! 

For this assignment, I needed to create a Content Management System using Sinatra and the CRUD, MVC framework. After recently moving to the beautiful island of Oahu, I decided it would be fitting to create a beach review app that would allow users to write reviews on beaches they have visited as well as view reviews from other visitors.  

Users can:
* Sign up, login, and logout
* Create a new review for an existing beach or create a review for a new beach
* Edit and delete reviews they created
* View all reviews in the app, even if they did not write them

After I had locked down my idea, I needed to figure out the structure. I decided I would need 3 models: user, beach, and review. 
* A user has many reviews and many beaches through reviews
* A beach has many reviews and many users through reviews
* A review belongs to a beach and a user

Views:
* Beaches: index for all beaches as well as show pages for each individual beach
* Reviews: index for all reviews, show pages for each review, new review form page, and edit review form page with a delete option
* Users: index or “home” page that lists all reviews created by that user

I struggled a bit with figuring out how the views should relate to the routes in the controllers, but reviewed the RESTful routing sections and determined the best way to implement in the app.

Overall, I had a lot of fun creating this app and hope to come back to it in the future to improve the layout and CSS styling.  I also think it would be great to add more sorting functionality, an average review for each beach, and a time of year column to the reviews table.


