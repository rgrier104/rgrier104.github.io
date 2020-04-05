---
layout: post
title:      "Advanced React Hooks: `useReducer`"
date:       2020-04-05 00:34:26 +0000
permalink:  advanced_react_hooks_usereducer
---


Today, I want to dive a little bit deeper into advanced React hooks, specifically: `useReducer`. `useReducer` is an advanced hook that allows you to manage state in functional components. It has a lot of similar functionality as Redux, but is automatically built in to React. You can find the official React docs that explain this hook [here](https://reactjs.org/docs/hooks-reference.html#usereducer).

### What exactly is `useReducer`?

`useReducer` is a hook that enables you to manage state, similar to `useState` (discussed a few posts back). `useReducer` is recommended if you have a more complex state, such as with nested objects or arrays, whereas `useState` is meant for more basic state management.

```
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

`useReducer` works very similarly to the [`reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) method in JavaScript used to essentially *reduce* a list to a single value. Like `reduce()`, it accepts a reducer function and an initial value/state. There’s also the optional third argument, `init` if you wish to initiate the initial state lazily (example in the React docs referenced above). It then returns the new state as well as a dispatch function. The reducer function receives the current state and an action and returns a new state. It's very similar to the reducer you would use in Redux, but it doesn’t necessarily need to follow the same formatting as Redux. Right now I'd prefer to stick with what I know, so I’ll be using Redux convention for my example. 

### `useReducer` vs Redux
Although `useReducer` can accomplish a lot of the same tasks as Redux, there are still times when Redux would be preferable, like when you have a large, complex application and wish to store your state in a centralized location rather than in individual components. In contrast, `useReducer` is a great alternative when you have a smaller application, but still want more control over managing complex state. 

### Example

I’m going to keep my example pretty simple for now. To continue with the Meal Planner App theme I’ve been using in my past few blog posts, I’ll create a component that allows you to add a recipe to the state. Here is the reducer - the same as my Redux reducer - with the case statement to add recipe:

```
function recipesReducer(state, action) {

  switch (action.type) {
    case 'ADD_RECIPE':
      return { ...state, recipes: [...state.recipes, action.payload] }
    default:
      return state
  }

}
```

Here is my Recipes component that includes a very basic form with an event handler that dispatches the action to the reducer to update the state when the form is submitted. The object format of my state is a bit overkill considering there's just a recipe name in the state, but I wanted to use the same Redux reducer I'm using in my current app without going crazy with the input fields for this example. 

```

const Recipes = () => {

  const [recipes, dispatch] = useReducer(recipesReducer, {recipes: []});
  
  function handleSubmit(e) {
    
    e.preventDefault();
    dispatch({
      type: "ADD_RECIPE",
      payload: {
        name: e.target.name.value
      }
    });
    e.target.name.value = "";
  }

  return (
    <>
      <form onSubmit={handleSubmit}>
        <input type="text" name="name" />
      </form>
      <ul>{recipes.recipes.map((item, index) => <li key={index}>{item.name}</li>)}</ul>
    </>
  );
}
```

References:
* https://daveceddia.com/usereducer-hook-examples/
* https://reactjs.org/docs/hooks-reference.html#usereducer

