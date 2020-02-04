---
layout: post
title:      "Cheat Sheet: How to create a new React-Redux app"
date:       2020-02-04 03:46:31 +0000
permalink:  cheat_sheet_how_to_create_a_new_react-redux_app
---

Creating a new React app can be overwhelming with all of the different packages you need to install and components you need to import in order to get everything set up and working properly. I decided to create a reference guide that documents the main npm packages and components needed to create a React-Redux single page app. Hopefully this guide will make the set-up process easier and faster in the future.

### `create-react-app` 
* First step to set up the basic file structure.

### `react-redux`
Resource: [React-Redux Documentation](https://react-redux.js.org/introduction/quick-start)

* **Provider:** Wraps the top level component and is responsible for passing the store down to all components that have been wrapped in the `connect()` function. Also responsible for alerting the Redux app to re-render when there is a change to state.

* **connect:** Responsible for connecting the component to the Redux store. It accepts 4 optional parameters: mapStateToProps, mapDispatchToProps, mergeProps, and options.

### `redux`
Resource: [Redux Documentation](https://redux.js.org/api/api-reference)

* **createStore:** Responsible for creating and returning an instance of the Redux store. It accepts a reducer, an initial state (optional), and an enhancer (optional).

* **applyMiddleware:** Allows you to incorporate middleware to your app, most commonly used to enable dispatch asynchronous actions -> in my case: `thunk`.

* **compose:** Composes functions from right to left, mostly used to apply multiple enhancers in a row. For reference, here is the code I used in my Traveller app to incorporate redux dev tools:

```
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

let store = createStore(tripReducer, composeEnhancers(applyMiddleware(thunk))
```

### `redux-thunk`
Resource: [Thunk README](https://github.com/reduxjs/redux-thunk)

* ** thunk:** Middleware responsible for handling asynchronous calls. Allows you to incorporate async code with Redux actions.

### `react-router-dom`
Resource: [React Router Documentation](https://reacttraining.com/react-router/web/guides/quick-start)

* **BrowserRouter:** Router component that wraps around App component to give all components access to the routes.

* **Route:** Responsible for rendering a specific component when the URL matches it’s path. It will have a `path` prop to define the URL path as well as a `component` or `render` prop to point to the desired component: `render` should be used when passing in an inline function, mainly used for when you need to pass props to the component. There are also 3 route props available: 


1. *match*: Contains information about how a route path matched the URL including `params`, `isExact`, `path`, and `url`. Mostly used to pass specific information like ‘id’ to a show component, allowing components to be used dynamically and ensuring the correct information is displayed.
2. *location*: Information about where the app is. It is never mutated unlike history.location, so it is best to the location object rather than history.location
3. *history*: Information about session history including length, push, and goBack. Ex: history.push can be used to redirect the user to a new page after a form submission.


* **Switch:** Component that wraps around Route components and renders only the first matching route. In this example below, “trips/new” only renders the TripInput component. Without Switch, “trips/new” would render both the TripInput component as well as the Trips component because the route “trips” can be found in both paths.

```
<Switch>
       <Route path="/trips/new" component={TripInput} />
       <Route path="/trips" render={(routerProps) => <Trips {...routerProps} trips={this.props.trips} />} />
</Switch>
```

* **NavLink:** Responsible for triggering routing by updating the URL and rendering the Route component. Allows for specific styling attributes that the basic Link component does not allow.



