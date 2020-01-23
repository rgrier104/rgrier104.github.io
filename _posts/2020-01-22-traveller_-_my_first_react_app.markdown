---
layout: post
title:      "TRAVELLER - My first React App"
date:       2020-01-23 03:04:28 +0000
permalink:  traveller_-_my_first_react_app
---


For my final Flatiron project, I created a travel planning app called Traveller. Traveller allows users to keep track of travel recommendations all in one place. Users can add relevant trips including completed, upcoming, and bucket list trips as well as add recommendations for future reference. Users can easily document any notes or recommendations for each trip as well as delete any recommendations they no longer find useful. This is the perfect app to store your favorite hotel, restaurant, and activity recommendations from past vacations as well as store miscellaneous recommendations received from friends for future travel. This app provides a single point of reference for all travel recommendations making it easily accessible when friends and family inevitably ask for travel recommendations as well as when you are finally ready to plan that dream vacation.

![Imgur](https://i.imgur.com/m9wyZpc.png)

## The Inspiration

I was inspired to create this app to solve a couple challenges I face:
* **Trouble recalling old trip recommendations**: A friend recently asked me about my trip to Japan last March. She’s planning a trip to Japan this year and wanted to know where to stay, where to eat, and what to do. Visiting Japan was a life-changing vacation for me, so I was thrilled to share my favorite experiences with her. There was just one problem - I had to dig through all of my old travel confirmations, photos, and unorganized itinerary to get all of the recommendations in order - not the easiest or most efficient process.

* **Scattered and unorganized notes/recommendations for future dream vacations**: I frequently read travel magazines to temporarily satisfy my wanderlust and help determine where I want to travel next. I also love getting travel recommendations from friends after they go on amazing vacations. I write down the hotels, activities, etc. that I’m interested in, but always forget where they are when the time comes to actually take the vacation.

Based on these challenges, I knew I needed a central location for all of my travel notes. A travel recommendation app was the perfect idea for my React project.

## Technical Details

Traveller is a web application with a React frontend and a Ruby on Rails backend API connected to a Postgres database. It utilizes the Redux library to connect to and modify any central state changes, Redux-Thunk middleware to allow asynchronous actions to be sent to the server, and React-Router to allow for easy navigation.

The backend Rails API has 2 models:
* Trip (data fields: name and status)
* Recommendation (data fields: title and description)

A trip has many recommendations and a recommendation belongs to a trip. A trip has a name and a status (completed, upcoming, or bucket list) and a recommendation has a title and a description. There is a lot of room for additional fields in these models, but I figured I’d start with the basics while I got the app up and running. There are active record validations included in the models to ensure only clean data is persisting to the Postgres database. I also added index, create, and destroy controller methods in order to perform the necessary actions on the database and return the relevant json to the client. 

The front-end is where things get interesting. I have created several Ruby on Rails apps at this point so that setup went relatively easy, but I knew the React app would be a much greater lift with this being my first React app. After running `create-react-app`, I needed to install the necessary packages to my package.json file including redux, react-redux, redux-thunk, and react-router-dom. 

When the app loads, the main Trip Container is rendered and trip data is fetched from the Rails API and stored in the Redux store. This trip information also contains the associated recommendations thanks to the serializer added to the backend. Interactions with the store are managed in a single reducer function, tripReducer. The reducer contains logic to update the state when trips are fetched or created and when recommendations are created or deleted.

The Navbar component contains the app header and NavLinks to allow users to easily navigate through the app by toggling between the different trip categories. The Trips Container is responsible for rendering the NavBar as well as defining the different route paths and subsequently rendering the corresponding components. The trips array in the Redux store is mapped to props in the Trips Container where it is then filtered based on the route and sent as props to the specified components. 

## Next Steps

In the interest of time, I created a MVP for version 1.0 of the Traveller App. In the future, I’d like to add the ability to edit trips and recommendations as well as incorporate additional fields that might be helpful such as recommendation type or trip dates. I also plan on adding user authentication and the ability to share trips and recommendations with other users directly in the app. 

Overall, I really enjoyed creating this app and applying my React skills into a fun application. The React library offers structure to my basic JavaScript knowledge and I’m excited to continue to build more complex React applications in the future.


