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
  ````
  render() {

  }
  ````

- step 4: ReactDOM.render - taking two arguments (MyComponent - so what we want to render) then where we want to render it (document.getElementById the react container)

````
ReactDOM.render(<MyComponent />,
document.getElementById('react-container'))

````

### Create class component

```sh
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

```sh
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

```sh
const MyComponent = () => {
    return <div>
            <h1>Hello World</h1>
            <p>This is my first React component!</p>
        </div>
}

ReactDOM.render(<MyComponent />,
    document.getElementById('react-container'))
```
