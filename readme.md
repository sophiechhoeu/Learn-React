# React Notes

  Understanding React through the creation of a bulletin Board notes message application

  ![bulletin board](https://github.com/sophiechhoeu/Learn-React/blob/master/images/Screen%20Shot%202018-01-07%20at%202.37.38%20am.png)

### References:
---
[Lydna Tutorial](https://www.lynda.com/React-js-tutorials/Welcome/519668/542808-4.html)

---

  ## Table of Contents

  * [Create React App through one file ](#create-react-app-through-one-file)

  * [Babel](#babel)

  * [Components](#components)

  * [Properties](#properties)

  * [Adding State](#adding-state)

  * [Using Refs](#using-refs)

  * [PropTypes](#proptypes)

  * [Adding Child Elements](#adding-child-elements)

  * [Update and Remove function](#update-and-remove-function)

  * [Adding New](#adding-new-notes)

  * [Keys As properties](#keys-as-properties)

    * WillMount, DidMount and Unmount

  * [Setting properties](#setting-properties)

  * [Updating Components](#updating-component)

  * [Lifecycle Methods](#lifecycle-methods)

* [Create react app through terminal](#create-react-app-through-terminal)
---

## What is React?

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

## Create React App through one file
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

[home](#table-of-contents)

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

[home](#table-of-contents)

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

[home](#table-of-contents)


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

[home](#table-of-contents)

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

[home](#table-of-contents)

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
[home](#table-of-contents)

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

[home](#table-of-contents)

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
[home](#table-of-contents)

## propTypes
optional feature
serves as documentation about how you wish your components to work, and what values you expect for them.

## Adding child elements
*make the board the parent of the note component*

add getInitialState method to Board - return an object where the key is notes and notes is an array


```
getInitialState () {
  return {
    notes: [
      'Call me',
      'Email me',
      'Eat Lunch',
      'finish proposal'
    ]
  }
},

```

then use map function to map over the notes array
then es6 arrow function to take two arguments (the notes and the item within the notes array)

return the note component with the key of {i} and then the content of the note {note}

Here we display notes dynamically based on the number of notes held in state

```
render() {
  return (
    <div className='board'>
    {this.state.notes.map((note, i) => {
      return <Note key={i}>{note}</Note>
    })}
    </div>
  )
}
```

[home](#table-of-contents)

## Update and Remove function

1. Update notes into objects

```
getInitialState () {
  return {
    notes: [
      {id: 0, note: 'Call me'},
      {id: 1, note: 'Email me'},
      {id: 2, note: 'Eat Lunch'},
      {id: 3, note: 'finish proposal'},
    ]
  }

```

2. Create Update method
- takes in newText and the Id
- create a notes variable, which will be the setstate of notes (this.state.notes) which will map over the array of notes.
- create a callback function to determine whether or not the note is going to be updated (with arrow syntax)
- check if the id of the note being edited has the same id
- if it isn't return the note otherwise return a new object
- the new object will push the keys in that note (... otherwise known as spread), setting the newText as the note
- then re set the state with all notes ({notes})

```
update(newText, id) {
  var notes = this.state.notes.map(
    note => (note.id !== id) ?
    note :
    {
      ...note,
      note: newText
    }
  )
  this.setState({notes})
},
```

3. Remove function - takes in id
- create variable called notes - set it to state and add filter method (this.state.notes.filter)
- **filter** will make a copy of the notes array and it will only return the items that passes
- add callback function which will check to see if the note id is not equal to the id (note.id !== id)
- In turn creating a new array that gets rid of the item that should be removed based on id.
- Then set the state to new notes where the item was removed this.setState({notes})
```
remove(id) {
  var notes = this.state.notes.filter(note => note.id !== id)
  this.setState({notes})
},
```

4. Each note method - will take in note
- this method handles returning our note component
- id - {note.id}, key - {note.id}
- when we're creating a note give it an onChange
{this.update}
- when we're removing a note git it onRemove
{this.remove}
- then the note will take on note value(note value from our key & values) {note.note}

```
eachNote(note) {
  return (
    <Note key={note.id}
    id={note.id}
    onChange={this.update}
    onRemove={this.remove}>
    {note.note}</Note>
  )
},
```

5. The notes will then display whatever the note text is.
- map over eachNote instead (this.eachNote)

```
render() {
  return (
    <div className='board'>
    {this.state.notes.map(this.eachNote)}
    </div>
  )
}
})
```

6. Attach update and remove methods to the note through save and remove

save - whenever on change is fired we want to pass the refs nextext value and the props id. (which is from the update method newText and id that we attached to the onChange property in eachNote)
reset the state to editing is false

```
save() {
  var val = this.refs.newText.value
  this.props.onChange(this.refs.newText.value, this.props.id)
  this.setState({editing: false})
},
```

remove - we attached remove to onRemove callback passing only the id.


```
remove(){
  this.props.onRemove(this.props.id)
},
```

[home](#table-of-contents)

## Adding new notes
found in the parent

the board is the parent of the note component

1. reset state to empty array

```
getInitialState () {
  return {
    notes: []
  }
},
```
2. Add method: takes in the text(also known as the newText)
inside this method create a variable called notes which will equal an array

first position is the the state of notes sent through spread(...). Use spread to take whatever the state of notes is 1 or 1000 and make it the first item in the array.

In this array we add a new object that includes the id and note. note set to text and id is nextID (the method that's created to handle the creation of a note id)

```
add(text){
  var notes = [
    ...this.state.notes,
    {
      id: this.nextId(),
      note: text
    }
  ]
  this.setState({notes})
},
```

3. nextId method - does this id exist or not, if not increment the id ++ (generate the id for me)
this.uniqueId equals a uniqueId or zero.

```
nextId(){
  this.uniqueId = this.uniqueId || 0
  return this.uniqueId++
},
```

then add

id: this.nextId(),

function to adding a new note

4. reset the state of notes outside of the array
this.setState({notes})

5. In render create a new button
on the onClick it takes a JSX expression that takes in a function ie  this.add function whenever onClick is used.   

```
<button onClick={() => this.add('New Note')}>+</button>
```

[home](#table-of-contents)

## Keys as properties

randomising notes positioning

*important - we need to pass a key property to our component when it is part of an array of children*

When something changes in react a re-render of what has changed will occur. If the children are dynamic ie (randomising or add new components to an array like spread) the re render might error. To prevent this we assign a key property.

In the note component (ie child)

1. add random function
x = x axis
y = y axis
s = units

this will return the random method which will generate a random number between certain numbers (0-1)

subtracting the x axis from the y axis will make this a number appear somewhere on our screen then add the units on the end.

```
randomBetween(x, y, s) {
  return (x + Math.ceil(Math.random() * (y-x))) + s
},
```

2. componentWillMount - will set up the style of the new note using this randomBetween function.

componentWillMount will fire before the render of DOM elements  

this.style will be an object where the right and top is equalled to the randomBetween function, passing in x, y, s

```
componentWillMount() {
  this.style = {
    right: this.randomBetween(0, window.innerWidth -150, 'px'),
    top: this.randomBetween(0, window.innerHeight -150, 'px')
  }
},
```

change CSS positioning to absolute

relative (means it will fall in line depending on
where it is added to the DOM )

3. In Render form and render Display
add this.style to the each div

Example:

```
renderForm() {
  return (
    <div className="note"
    style={this.style}>
    <textarea ref="newText"></textarea>
    <button onClick={this.save}>SAVE</button>
    </div>
  )
},
```

[home](#table-of-contents)

## Component Lifestyle

provides the hooks for the creation, lifetime and teardown of components



### Mounting Lifestyle
* getInitialState - called once and will set the default for the state

* componentWillMount - called before the render and it's the last chance to effect state prior to render

* render - required method

* componentDidMount - fired after the render so after a successful render we can access the dom, the component has been rendered and the user can interact with it

**Updating**

* componentWillReceiveProps - we get the opportunity to change object and effect state.

* shouldComponentUpdate/ componentWillUpdate - invoked before rendering and used for optimisation (only called if something has changed)

* render - required method and part of the update lifecycle

* componentDidUpdate - fire right after everything in the Dom has been updated

* componentWillUnmount - called before the component is unmounted. If called on the parent the children will be unmounted as well.

**componentWillUnmount**

on the click of the component we're unmounting the component

1. find the element (ie myDiv)
then on the onclick we're calling the unmountComponentAtNode function which references the parent div

```
var getRidOfBox = document.getElementById('myDiv')
getRidOfBox.onclick = function(){
  ReactDOM.unmountComponentAtNode(
    document.getElementById('react-container'))
    alert('component is unmounted')
}
```
[home](#table-of-contents)

## Setting Properties

Get default props will be called once the component renders

returns an object with our style properties

```
getDefaultProps() {
  return {
    backgroundColor: 'red',
    height: 200,
    width: 200
  }
},
```

setting this default allows reuse over style again through this.props

it initialises default properties for our components

not a required method but great for usability.

```
return (
  <div id='myDiv'>
  <div style={this.props}></div>
  <section style={this.props}></section>
  </div>
)
```
[home](#table-of-contents)

## Updating Components

Use getInitialState() with style properties

Meaning when the application renders it will returns the initial state

```
getInitialState() {
  return {
    backgroundColor: 'red',
    height: 200,
    width: 200
  }
},
```

amend render to only one overarching div
change style property to this.state

```
render(){
    return (
      <div style={this.state}
        onClick={this.update}>
      </div>
    )
}
```

The update method handles an changes that occurred to the div

The update affects the state, returning an object that a backgroundColor that is grey (initially red )

attach to div with onClick property

```
update() {
  this.setState({backgroundColor: 'grey'})
},
```

Component did update fires after a **successful** re-render

change in state will occur -> component re-render -> component did update will be called.

```
componentDidUpdate(){
  alert("component updating");
},
```

[home](#table-of-contents)

## Lifecycle methods

- Add defaultValue and this.props.children in the text area

```
renderForm() {
  return (
    <div className="note"
    style={this.style}>
    <textarea ref="newText"
    defaultValue={this.props.children}></textarea>
    <button onClick={this.save}>SAVE</button>
    </div>
  )
},
```

- componentDidUpdate: add to note component between componentwillmount and randomBetween to be called right after an update

This method is checking to see if the state is editing if it's true it will focus on the newText and select it

```
componentDidUpdate(){
  if (this.state.editing) {
    this.refs.newText.focus()
    this.refs.newText.select()
  }
},
```

- shouldComponentUpdate: after component did update, to allow to switch between states.

takes in new props and new state and if changes happen the component will update if nothing has happened no re-render will take place.

```
shouldComponentUpdate(nextProps, nextState) {
  return this.props.children !== nextProps.children || this.state
  !== nextState

},
```

- Board component

add variable url for api
add fetch(url)
.then a callback function will show json api data.
.then first position in the array
.then split the text based on a period
.then send an array and then foreach on the array send a sentence and use the this.add function (sentence represents text) then add catch as a fail safe on an error  

```
componentWillMount() {
  if (this.props.count) {
    var url = `https://baconipsum.com/api/?type=all-meat&sentences=${this.props.count}`
    fetch(url)
      .then(results => results.json())
      .then(array => array[0])
      .then(text => text.split('. '))
      .then(array => array.forEach(
        sentence => this.add(sentence)))
        .catch(function(err) {
          console.log("didnt connect", err)
        })
  }
},
```

- render for note under render display
add react draggable component wrapped around what we want to edit, this.state.editing
wrapped in a jsx expression

- ternary operator ? :
(condition) ? value1:value2

```
render () {

  return ( <ReactDraggable>
    {(this.state.editing) ? this.renderForm() : this.renderDisplay()}
    </ReactDraggable>
    )
  }
})
```
[home](#table-of-contents)

## Create react app through terminal
*through terminal*
* launching bulletin board via create react app

- *make sure node is installed*
- *make a directory - cd into directory*
- *create-react-app (name of app)*
- *terminal will ask to cd into app folder then run yarn start*

install

```
$ npm install create-react-class

```
amend React.createClass to createReactClass as part of 16 update

Add board component to app.js
remove component from import React
remove logo
update export default board
rename app.js to board.js
add import Note from './Note'
create note.js file
add note component
add import react from react and css to note component
add export default note

install
```
$npm install --save react-draggable
```

add  import draggable from react-draggable to note
update draggable component tag from react draggable to draggable only in the return render

open index.js
update app to import Board from Board  
under render with Board commponent and note count, then update root to react-container

index.html update div from root to react-container

remove index css (may conflict)

then in terminal

```
npm start
```
npm run build in terminal will create a production build folder that minifies our js etc

[home](#table-of-contents)
