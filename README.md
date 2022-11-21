# GifExpertApp

![Demo](./public/GifExpertApp.gif)

## To execute the project:

- Clone this repo
- ```cd react-gif-expert/```
- ```npm install```
- ```npm run dev```
- Open the terminal link

You can see the link of the project [here](https://gif-expert-leodev.netlify.app/) 

What I learned:

- How to handle events.
- How to use the hook of useState.
- How to communicate between different components.
- It is important to keep in mind that each element in this case of the array must have a unique key.
- Functions should not be invoked inside a funtional component because every time the component is re-rendered it will execute the functions again.
- How to make API requests in React

**Note**: this project is created with [Vite](https://main.vitejs.dev/guide/) and React, Vite is a compiler tool that is much faster than [Create React App](https://create-react-app.dev/).

The following are some notes from what we learned while building the application:

## Hook useState

Allows for stateful values and a function to update these states.

To use useState you need the following:

1. Import it from the React library.
2. Invoke it inside the React component.

```jsx
import { useState } from "react";

const [state, setState] = useState(initialValue)
```

1. The state is then rendered or setState can be called to update the state value.

## Communication between components

Communication between components is done through **props**, to pass information from a parent component to a child component. For that it is necessary to create a custom attribute in the child component tag that is declared in the parent tag.

In this app it is observed when the AddCategory is called in the GifExpertApp.jsx:

```jsx
//GifExpertApp.jsx
import { useState } from "react";
import { AddCategory } from "./components/AddCategory";

export const GifExpertApp = () => {

    const [categories, setCategories] = useState([ 'One Punch', 'Dragon Ball' ]);

    const onAddCategory = ( newCategory ) => {;
        setCategories([ newCategory, ...categories]);
    };

  return (
    <>
        <h1>GifExpertApp</h1>
        <AddCategory onNewCategory={ onAddCategory } />

        <ol>
            {
                categories.map( category => {
                    return <li key={ category }> { category } </li>
                })
            }
        </ol>
    </>
  )
}
```

In the child component this data is received through the parameter of the function that controls the component. These parameters are received in object form but for this case destructuring was performed.

```jsx
//AddCategory.jsx

export const AddCategory = ({ onNewCategory }) => {

    const [inputValue, setInputValue] = useState('');

    const onInputChange = (event) => {
        setInputValue( event.target.value );
    }

    const onSubmit = (event) => {
        event.preventDefault();
        if(  inputValue.trim().length <= 1 ) return;
        onNewCategory(inputValue.trim());
        setInputValue('');
    }

  return (
    <form onSubmit={ onSubmit }>
        <input 
            type="text"
            placeholder="Buscar gifs"
            value={ inputValue }
            onChange={ onInputChange }
        />
    </form>
  )
}
```

With this, the event can be called and the communication between components can be carried out.

## Use Effect

It is a hook used to trigger secondary effects

useEffect is a tool that allows us to interact with the outside world but does not affect the rendering or performance of the component it is in.

The useEffect only returns a function and not a promise.

## Useful links

[Strict Mode - React](https://es.reactjs.org/docs/strict-mode.html)

[Hooks API Reference - React](https://es.reactjs.org/docs/hooks-reference.html#useeffect)

[The React useEffect Hook for Absolute Beginners](https://www.freecodecamp.org/news/react-useeffect-absolute-beginners/)

[useState](https://reactjs.org/docs/hooks-reference.html#usestate)

[React Hooks for Beginners – Learn to Use the useState Hook in 10 Minutes](https://www.freecodecamp.org/news/learn-react-usestate-hook-in-10-minutes/)