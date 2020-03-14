---
layout: post
title:      "React Hooks"
date:       2020-03-14 21:56:25 +0000
permalink:  react_hooks
---


Lately, I’ve read a lot about the new React hooks functionality and figured it would be a great topic for a blog post. I’m also starting to refactor my Meal Planning Application using React vs vanilla JS and want to make sure I’m using the latest and greatest functionality from React. 

## What are hooks? 
At a high level, it’s actually fairly simple: hooks are functions that allow you to use state and lifecycle methods in functional components. Prior to hooks, which became available in v16.8, you would need to use a class component if you wanted to manage state within the component. Although the functionality to manage state using class components won’t be going away any time soon, it’s recommended that you start utilizing hooks in your new React applications going forward. 

## Why use hooks?
There are several reasons why you should use hooks which you can read about [here](https://reactjs.org/docs/hooks-intro.html#motivation).  In my opinion, the best reason is that hooks allow you to reuse stateful logic between components. Before hooks, you could use higher-order components or render props to achieve this functionality. However, the implementation requires you to restructure your components which can, as the React docs put it, put you in ‘wrapper hell.’ It’s also nice to not have to rewrite your component if you realize you need to manage state after already writing a functional component.

## Example using `useState`

One common hook that has been introduced is `useState` which allows you to add state to functional components. Here is a basic example of how I might apply this hook in my Meal Planner App using a controlled form to add a new recipe.

### Without hooks

```
class RecipeForm extends React.Component {
    state = {
        value: '',
    }

    handleSubmit = (event) => {
        event.preventDefault()
        this.props.addRecipe(this.state)
        this.setState({
            value: '',
        })
    }

    handleChange = (event) => {
        this.setState({
            value: event.target.value
        })
    }

    render() {
        return (
            <form onSubmit={this.handleSubmit}>
                <input
                    type="text"
                    value={this.state.value}
                    onChange={this.handleChange}
                />
            </form>
        )
    };
}
```

### With hooks

```
function HookRecipeForm({ addRecipe }) {
    const [value, setValue] = useState("");

    const handleSubmit = e => {
        e.preventDefault();
        addRecipe(value);// code to actually add recipe to state
        setValue("");
    };

    return (
        <form onSubmit={handleSubmit}>
            <input
                type="text"
                value={value}
                onChange={e => setValue(e.target.value)}
            />
        </form>
    );
}
```

With `useState`, you declare the state variable as well as the function that updates it (value and setValue in this case) and pass along the initial state as an argument to `useState`. There are also ways to write your own custom hooks in order to easily reuse that functionality throughout mulitple components, but I’ll save that for a separate blog post. 

