---
layout: post
title:      "Redux Hooks"
date:       2020-03-22 01:50:29 +0000
permalink:  redux_hooks
---


To follow up on my last blog post on React Hooks, I wanted to dig a little deeper into how to use Hooks with Redux. It turns out that you can connect to the Redux store and dispatch actions without using the `connect()` Higher Order Component! You still want to wrap the app in `<Provider>` tags and pass in the store, but you can now access the store using the new hooks `useSelector` and `useDispatch`.

## `useSelector`

This hook is very similar to the `mapStateToProps` argument in `connect()`. You can pass in a selector function as an argument that returns the piece of the Redux store state that you want to include in your component. There are a few ways in which `useSelector` is different from `mapStateToProps` that you should read more about in the React Redux documentation [here](https://react-redux.js.org/api/hooks#useselector). One difference is `useSelector` uses strict reference comparison when determining if a re-render is needed whereas `mapStateToProps` uses shallow equality. You can pass the React-Redux function, `shallowEqual`, to `useSelector` as a second argument in order to use shallow rather than strict equality. 

I decided to try out `useSelector` in my meal planning application rebuild. I have a Recipes component that needs to access all recipes stored in the Redux store state. Instead of the normal `connect()` and `mapStateToProps` combo, I used `useSelector` below:

```
import React from 'react';
import { useSelector } from 'react-redux';

const Recipes = () => {

    const recipes = useSelector(state => state.recipes)

    return (
        <div>
            <ul>
                {recipes.map(recipe => <li key={recipe.id}>{recipe.name}</li>)}
            </ul>
        </div>
    )
}

export default Recipes;
```

## `useDispatch`

This hook essentially replaces the `mapStateToDispatch` argument in `connect()`. It returns the dispatch method from the Redux store so you can dispatch actions. I tested this out in my App component where I dispatch the `fetchRecipes` action on mount, so the Redux store has an updated state that includes all of the recipes from the Rails API. In order to call this dispatch action on mount, I implemented the `useEffect` hook to replace `componentDidMount`. I won’t get into the details here, but the [React docs](https://reactjs.org/docs/hooks-effect.html) explain it thoroughly if you want to more information.

```
import React, { useEffect } from 'react';
import { useDispatch } from 'react-redux';
import { fetchRecipes } from './actions/fetchRecipes';
import Recipes from './components/Recipes';
import MealPlan from './components/MealPlan';

const App = () => {

  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(fetchRecipes())
  },[dispatch])

    return (
      <div className="App">
        <h1>Meal Planner</h1>
          <MealPlan />
          <Recipes />
      </div>
    );
}

export default App;
```

React-Redux also provides a `useStore` hook which returns a reference to the Redux store. However, it is recommended that you avoid using this hook if possible and to stick to `useSelector`.

I’m really excited to be using the new React-Redux Hooks functionality in the rebuild of my meal planner app. It’s a fun way to stay up to date with React. You can follow along with my progress here: https://github.com/rgrier104/meal-planner-react.
