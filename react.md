# React

<img src="https://cdn.worldvectorlogo.com/logos/react.svg" width=128px>

## Generating a React Project

1. Install the create-react-app program globally
`sudo npm install -g create-react-app`

2. Run create-react-app with the name of the app from the project folder
`create-react-app jsx`

## Customizing the initial app directory

1. Delete all of the code inside the src folder
2. Add a single index.js file
3. Inside the index.js put the following:

```
// import the React and ReactDOM libraries
import React from 'react'
import ReactDOM from 'react-dom'

// Create a react component
const App = function() {
    const buttonTest = 'Click Me!'

    return (
        <div>
            <label className="label" for="name">Enter Name:</label>
            <input id="name" type="text" />
            <button style="{{ backgroundColor: 'blue', color: 'white' }}">Submit</button>
        </div>
}

/// Take the react component and show it in the browser
ReactDOM.render(
    <App />,
    document.querySelector('#root')
)

```

## JSX

### Converting HTML to JSX

#### Original HTML

```
<div>
  <label class="label" for="name">Enter Name:</label>
  <input id="name" type="text" />
  <button style="background-color: blue; color: white;">Submit</button>
</div>
```

#### JSX Conversion

```
<div>
  <label className="label" for="name">Enter Name:</label>
  <input id="name" type="text" />
  <button style="{{ backgroundColor: 'blue', color: 'white' }}">Submit</button>
</div>
```

#### Inline styling

Inline styles should be surrounded by double curly brackets. Hyphenated keywords should remove the hyphen and change the keyword to camel case. Value are wrapped in single quotes. Multiple values are separated with a comma.

__HTML__
`<div> style="background-color: blue; color: white;"></div>`

__JSX__
`<div style={{ backgroundColor: 'blue', color: 'white' }}></div>`

#### Classes

Instead of class use className.

__HTML__
`<label class="label" for="name">Enter Name:</label>`

__JSX__
`<label className="label" for="name">Enter Name:</label>`

#### Referencing Variables

Javascript variables can be referenced by surrounding with single curly brackets. You can also call functions from within the curly brackets.

`<button style="{{ backgroundColor: 'blue', color: 'white' }}">{ buttonText }</button>`

[Back to Index](index.md)
