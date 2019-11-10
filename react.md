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

#### What variables JSX can't show

Objects can not be directly displayed as text in JSX such as `buttonText = {text: 'Click Me' }`. However members can be accessed and printed.  Object can be used in JSX as long as they are not printed directly in the rendered HTML.

## Props

### Component Nesting

Showing a component inside of another component

### Component Reusability

Make a component that is reusable

1. Identify the JSX that appears to be duplicated
2. Think of a name for what the block of JSX does
3. Create a new file to house the new component
4. Create a new component in the new file and paste the JSX into it
5. Make the component configurable using props

### Component Configuration

Being able to configure a component when it is created

### Passing Props to a component (attributes)

1. In the call to the component pass an attriibute:
    `<CommentDetail author="Sam" />`
2. In the component, refer to the attribute via the props object:
    `<a href="/" className="author">{props.author}</a>`

### Passing Props to a component (Child Rendering)

1. In the parent Component call nest the content between the opening and closing tags.
    `<ApprovalCard>This is a message</ApprovalCard>`
2. In the component the nested info is passed in a props.children, which can be used a an object in the JSX
    `<div>{props.children}</div>`

### Specifying Default Properties

You can specify default properties as follows:
`ComponentName.defaultProps = { property: value }`

If you don't specify that property the default value will automatically be used.

## Class Based Components

Class based components contain the following:

1. They are javascript classes that extend from React.Component
2. The **must** have a render function or you will get an error
    `TypeError: instance.render is not a function`
3. They can contain the following functions:
    * `constructor(props)` - runs once on creation and is where a state object can be created
    * `componentDidMount()` - runs once when the component is created
    * `componentDidUpdate()` - runs everytime the state is updated
    * `componentWillUnmount()` - runs when component is about to be destroyed

```javascript
class App extends React.Component {
  constructor (props) {
    super(props);

    this.state = {
      lat: null,
      errorMessage: ''
    }
  }
  
  componentDidMount() {
    console.log('componentDidMount just ran...')
    window.navigator.geolocation.getCurrentPosition(
      position => {
        this.setState({lat: position.coords.latitude})
      },
      err => this.setState({errorMessage: err.message})
    )
  }

  componentDidUpdate() {
    console.log('componentDidUpdate just ran...')
  }

  render() {
    if (this.state.errorMessage && !this.state.lat) {
      return <div>Error: {this.state.errorMessage}</div>
    }
    if(!this.state.errorMessage && this.state.lat) {
      return <div>Latitude: {this.state.lat}</div>
    }

    return <div>Loading...</div>
  }
}
```

[Back to Index](index.md)
