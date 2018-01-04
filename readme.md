# React Notes

[Lydna Tutorial](https://www.lynda.com/React-js-tutorials/Welcome/519668/542808-4.html)

- Javascript Library created by Facebook to help developers and designers build user interfaces quickly.

- open source

- Benefits: developing a large scale single page application easier

- Virtual Dom : High speed virtual  DOM ie whenever a change happens, the virtual DOM efficiently re-renders

- Functional Programming : ie the emphasis on function composition over object orientation

- immutable data: ie creating copies of objects and replace them instead of mutating the originals

- DOM: react renders the DOM rapidly. The DOM or document object model is the structure of HTML elements that make up a webpage. It also refers to the **API** for how these page elements are accessed and changed.

Reading and writing to the DOM is slow because it affects the application speed. Reading and writing to Javascript objects is faster, React has a virtual DOM that writes to the browser DOM only when it needs to.

**DOM updates are only made if there has been some sort of change**

*get Element by ID* - reading from the DOM.

*change one of those elements* - classes, content, you are writing to the DOM

with React

*it only interacts with the virtual DOM, so when we call the render function, React will update the virtual DOM only pushing the necessary changes to the real DOM*

- DOM

- React Virtual DOM

- Javascript Logic

## Create React App
*message board react application*

- create index.html

### index.html

*in-browser transpiling*
In the head add react script developer tags for react and react DOM.

```sh

<script src="https://fb.me/react-15.2.1.js"></script>
<script src="https://fb.me/react-dom-15.2.1.js"></script>

```

- add another script tag which will house all the React content

- this will contain a function called ReactDOM.render
which will take two arguments:
 1. React.createElement: the type of element we want to create ('div'), pass it some properties( null ) and a child element ('Hello World').
 2. document.getElementById: where want to put this div that we've created sending it in a react-container

```sh

<body>
  <div id='react-container'></div>
  <script>
    ReactDOM.render(
      React.createElement('div', null ,'Hello World'),
      document.getElementById('react-container'))
  </script>

```

Using JSX but errors - what we need Babel for this to run

```sh

<div id='react-container'></div>
<script>
  ReactDOM.render(
    <ul>
    <li>item 1</li>
    <li>item 2</li>
    <li>item 2</li>
    </ul>,
    document.getElementById('react-container'))
</script>

```

## Babel

Transpiler that will transpile Javascript Code.
It works for JSX and also works for es6 and beyond

Babel transpiles it into something that the browser can use straight away.
JSX to a createElement Function call.

Below is in-browser transpiling - best practice is to use webpack to include Babel as a module.

```sh
<head>
  <script src="https://fb.me/react-15.2.1.js"></script>
  <script src="https://fb.me/react-dom-15.2.1.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
  <title>My First React File</title>
</head>

```

then add type="text/babel" so it knows to transpile this code

```sh
<script type="text/babel">
  ReactDOM.render(
    <ul>
    <li>item 1</li>
    <li>item 2</li>
    <li>item 2</li>
    </ul>,
    document.getElementById('react-container'))
</script>
```


## Components

React applications = collection of Components
Components are small user interface elements that display data as it changes over time.

- Step 1: set the variable for the component (var = MyComponent)
- Step 2: React.createClass will take in a function with an object ({})
- Step 3: first method will be render (always required when we create a component because it tells react what we want to render to the DOM)
  ```
  render() {

  }
  ```

- step 4: ReactDOM.render - taking two arguments (MyComponent - so what we want to render) then where we want to render it (document.getElementById the react container)

```
ReactDOM.render(<MyComponent />,
document.getElementById('react-container'))

```

### Create class component

```javascript
<div id='react-container'></div>
<script type="text/babel">
  var MyComponent = React.createClass({
    render() {
      return <div>
      <h1> Hello World</h1>
      <p>This is my first react component</p>

      </div>
    }
  })

  ReactDOM.render(<MyComponent />,
  document.getElementById('react-container'))
</script>
```

### Es6 class syntax

```javascript
<div id='react-container'></div>
<script type="text/babel">

  class MyComponent extends React.Component {
    render() {
      return <div>
      <h1> Hello World</h1>
      <p>This is my first react component</p>

      </div>
    }
  }

  ReactDOM.render(<MyComponent />,
  document.getElementById('react-container'))
</script>
```


### Stateless functional component

ie a simple function that returns react elements
uses es6 arrow syntax ie

````
const MyComponent = () => {

}
````

Most common in react documentation

```Javascript
const MyComponent = () => {
    return <div>
            <h1>Hello World</h1>
            <p>This is my first React component!</p>
        </div>
}

ReactDOM.render(<MyComponent />,
    document.getElementById('react-container'))
```

## Properties

- this.props.text - JSX syntax wrapped in curly braces
- React wants to render only  one element so wrap multiple components in one div.
- display dynamic properties and reuse components

```javascript
<div id='react-container'></div>
<script type="text/babel">
    var MyComponent = React.createClass({
      render() {
        return <div>
                <h1>{this.props.text}</h1>
                <p>This is my first React component!</p>
            </div>
      }

    })

    ReactDOM.render(
      <div>
      <MyComponent text="Hello World" />
      <MyComponent text="I am a component" />
      <MyComponent text="I have been reused" />
      </div>,
        document.getElementById('react-container'))

</script>

```

### props.children

- help display some dynamic content
- added closing my component tag </MyComponent>
- by doing so, you can add tags or text inside of these components creating components that are wrapped around child text.
- to display children replace the static content with another JSX expression {this.props.children}
- {this.props.children} : looking for the child of this particular element and display that inside the paragraph


```javascript
<div id='react-container'></div>
<script type="text/babel">
    var MyComponent = React.createClass({
      render() {
        return <div>
                <h1>{this.props.text}</h1>
                <p>{this.props.children}</p>
            </div>
      }

    })

    ReactDOM.render(
      <div>
      <MyComponent text="Hello World" >This is message 1</MyComponent>
      <MyComponent text="I am a component" >This is message 2</MyComponent>
      <MyComponent text="I have been reused">This is message 3</MyComponent>
      </div>,
        document.getElementById('react-container'))

</script>
```

## React Events
- create variable called Note
- use

  ```javascript
  React.createClass({

  })
  ```
- each components needs a render function that says what we want to return

  ```javascript
  render() {
    return (

      )
  }
  ```
- best practice for render method is to wrap all of the DOM elements that we want to create in parentheses () otherwise it will error

- JSX classes are <div **className**="">

- then ReactDOM.render function takes in two components what we want to render(<Note></Note) and where document.getElementById('react-container')

```javascript
  ReactDOM.render(<Note></Note>,
  document.getElementById('react-container'))
```

- create edit and remove functions

```javascript
edit() {
   alert("edit note")
},
```
***same for remove***

- adding event by: onClick={} to each button
    ***{} for JSX expression***
    ```javascript
    onClick={this.edit}
    onClick={this.remove}
    ```
- displaying note content: add text inside the render component
- in the render inside the return and the div
```
render () {
  return (
    <div className="note">
    <p>{this.props.children}</p>
    <span>
      <button onClick={this.edit}>EDIT</button>
      <button onClick={this.remove}>X</button>
    </span>
    </div>
  )
```





## React State
[Checkbox](/checkbox/index.html)

- When a component's state data changes, the render function will be changed again to re-render the change in state

- create Checkbox variable with ***React.createClass({
})*** this will simply introduce state

- then
```
 render(){

  }
```
- then
```
return (
    <div>
    </div>
  )
```

- inside the div create an input type

```
<input type="checkbox"/>
```

- add react state: getInitialState ie when the component renders this will be the initial state(unchecked) where {checked:false}
```
getInitialState() {
  return {checked: false}
}
```

- custom method handleCheck (or whatever you want to name it) here we use this.setState. So whenever handleCheck is called it's going to set the state to something different


- setState takes an object then references our state variable ie checked(from initial state) then check its not this.state checked allowing toggle functionality

```
handleCheck() {
  this.setState({
    checked: !this.state.checked
  })
}
```

- attach state to the DOM elements we do this by adding onChange property which will take a JSX expression {this.handleCheck}
```
onChange={this.handleCheck}
```

- add var msg and add {msg}
- create if statement that asks if(this.state.checked) ie true then the message should be displayed as checked and vice versa

```
var msg
if (this.state.checked) {
  msg = "checked"
} else {
  msg = "unchecked"
}
return (
 <div>
 <input type="checkbox"
   onChange={this.handleCheck}
   />
 <p>This box is {msg}</p>
 </div>
)

```

- add defaultChecked = to a JSX express {this.state.checked}

- this.setState is the function we call every time we what to change the state

```javascript
<div id='react-container'></div>
<script type="text/babel">
  var Checkbox = React.createClass({
    getInitialState() {
      return {checked: true}
    },
    handleCheck() {
      this.setState({
        checked: !this.state.checked
      })
    },
    render() {
       var msg
       if (this.state.checked) {
         msg = "checked"
       } else {
         msg = "unchecked"
       }
      return (
        <div>
        <input type="checkbox"
          onChange={this.handleCheck}
          defaultChecked={this.state.checked}
          />
        <p>This box is {msg}</p>
        </div>
      )
    }
  })
  ReactDOM.render(<Checkbox/>,
    document.getElementById('react-container'))
</script>
```

## Adding state
[note](/bulletinBoard/index.html)

- initial state to false
- edit function state is true meaning every time this edit method is called we set the state to true.
```
getInitialState() {
  return{editing:false}
},
edit(){
   this.setState({editing:true})
},
```

- create method for save.
- save will be a button on the form that changes the editing state back to false and displays the note.
```
save() {
  this.setState({editing:false})
},

```

- create two methods one: render the form two: render display the note. Render method determines which will be displayed

- So if editing is true (this.state.editing) ?
if true we're going to render the form :
if false  render the display.



```
renderForm() {
  return (
    <div className="note">
    <textarea ref="newText"></textarea>
    <button onClick={this.save}>SAVE</button>
    </div>
  )
},

renderDisplay() {
  return (
    <div className="note">
    <p>{this.props.children}</p>
    <span>
      <button onClick={this.edit}>EDIT</button>
      <button onClick={this.remove}>X</button>
    </span>
    </div>
  )
},
render () {

  return (this.state.editing) ? this.renderForm() : this.renderDisplay()
  }
})

```

## Using refs
grabbing the value of elements through refs

to grab the value of the text inorder to save:
add ref="newText"
```
<textarea ref="newText"></textarea>
```

- update save method
create variable called val
```
var val = this.refs.newText.value

```
