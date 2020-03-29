---
layout: post
title:      "Creating a Weekly Calendar Using React"
date:       2020-03-29 00:40:43 +0000
permalink:  creating_a_weekly_calendar_using_react
---


This week, I continued to rebuild my Meal Planner App and needed to determine the best way to create the weekly calendar view to display the full meal plan in React. I figured it’d be a great opportunity to write a blog post with some refreshers on rendering React components. For the calendar, I needed:
* 7 day containers: one for each day of the week
*  4 meal category containers within each day: breakfast, lunch, dinner, snack

The user would be able to click on the specific meal for the desired day and a modal would popup with a drop down list of all recipes to choose from. They would select the recipe and it would be saved to the meal plan. 

Thankfully, this is significantly easier to create using React components compared to vanilla JavaScript! My original code in my first JS project was extremely messy and confusing to follow as I needed to manipulate the DOM to create each HTML element. Each day container would essentially look the same, so rather than repeating a ton of code, I decided to simply create one `DayCard` component and one `MealCard` component. I created an array with all of the days of the week that I could loop through to render the DayCard component 7 times. I did the same for meals within the` DayCard` component. The final product looks something like this:

#### DayCard

```
import React from 'react';
import DayCard from './DayCard';

const MealPlan = () => {

    const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

    return (
        <div>
            {days.map(day => <DayCard day={day} key={day} />)}
        </div>
    )
}

export default MealPlan;
```

#### MealCard

```

import React from 'react';
import MealCard from './MealCard';

const DayCard = ({ day }) => {

    const meals = ["Breakfast","Lunch","Dinner","Snack"]

    return (
        <div>
            <h3>{day}</h3>
            {meals.map(meal => <MealCard meal={meal} key={meal} />)}
        </div>
    )
}

export default DayCard;
```

Next, I needed to create a modal that pops up when a user clicks the 'select meal' button. The easiest way to do this is by adding state to the `MealCard` component that updates if the 'select meal' button has been clicked. Using React hooks, adding state can look something like this:
```
    const [show, setShow] = useState(false);
    const openModal = () => setShow(true);
    const closeModal = () => setShow(false);
```
You can call the `openModal` and `closeModal` functions on click to update the state.  [This article](https://reactgo.com/react-modal-tutorial/) provides a great walkthrough of how to implement using React hooks and includes CSS styling! 

Here are some screenshots of my app with the calendar view and modal - please excuse the lack of styling, I'll be adding that later :)

![Imgur](https://i.imgur.com/06dvzi6.png?1)
![Imgur](https://i.imgur.com/LJ2mbuu.png?1)
