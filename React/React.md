https://github.com/StephenGrider/cheatsheets/blob/master/react.md


# React.js
- Components (Class components, Functional Components)
- Properties
- State
- Children
- 


 
## Components
```jsx
import React from 'react'
import ReactDOM from 'react-dom';

//Functional components
const App=(props)=>{
    return(<div>{props.children}</div>)
}
 

ReactDOM.render(
        <App/>,
        document.getElementById('main')
);
```
 

```jsx
//Class components
class Hello extends React.Component {
  render () {
    return <div className='message-box'>
      Hello {this.props.name}
    </div>
  }
}
```

 

  
### Properties
```javascript
...
```

### States
```javascript
...
````
### Children
```javascript
...
````

### Defaults
See: [defaultProps](https://reactjs.org/docs/react-component.html#defaultprops)
```jsx
// Setting default props
Hello.defaultProps = {
  color: 'blue'
}
```
  
See: [Setting the default state](https://reactjs.org/docs/react-without-es6.html#setting-the-initial-state)

 

## Functional components
See: [Function and Class Components](https://reactjs.org/docs/components-and-props.html#functional-and-class-components)


## Pure components
See: [Pure components](https://reactjs.org/docs/react-api.html#react.purecomponent)  
Performance-optimized version of `React.Component`. Doesn't rerender if props/state hasn't changed.

```jsx
import React, {PureComponent} from 'React/React'

class MessageBox extends PureComponent {
···
}
```
 



### Component API
These methods and properties are available for `Component` instances.   
See: [Component API](http://facebook.github.io/react/docs/component-api.html)

```jsx
this.forceUpdate()
this.setState({ ... })
this.setState(state => { ... })
```

```jsx
this.state
this.props
```


## Lifecycle

--- 
See: [Component specs](http://facebook.github.io/react/docs/component-specs.html#updating-componentwillreceiveprops)


### Mounting

| Method | Description |
| --- | --- |
| `constructor` _(props)_ | Before rendering [#](https://reactjs.org/docs/react-component.html#constructor) |
| `componentWillMount()` | _Don't use this_ [#](https://reactjs.org/docs/react-component.html#componentwillmount) |
| `render()` | Render  [#](https://reactjs.org/docs/react-component.html#render) |
| `componentDidMount()` | After rendering (DOM available) [#](https://reactjs.org/docs/react-component.html#componentdidmount) |
| --- | --- |
| `componentWillUnmount()` | Before DOM removal [#](https://reactjs.org/docs/react-component.html#componentwillunmount) |
| --- | --- |
| `componentDidCatch()` | Catch errors (16+) [#](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html) |

Set initial the state on `constructor()`.
Add DOM event handlers, timers (etc) on `componentDidMount()`, then remove them on `componentWillUnmount()`.

### Updating

| Method | Description |
| --- | --- |
| `componentDidUpdate` *(prevProps, prevState, snapshot)* | Use `setState()` here, but remember to compare props |
| `shouldComponentUpdate` *(newProps, newState)* | Skips `render()` if returns false |
| `render()` | Render |
| `componentDidUpdate` *(prevProps, prevState)* | Operate on the DOM here |

Called when parents change properties and `.setState()`. These are not called for initial renders.

## HOC - High Order Component
HOC it is a function that accepts a component and wrap it in some logic.

```javascript

const RecordsList = withSubscription(CommentList, getUsersFN);
const CommentsList = withSubscription(CommentList, getCommentsFN);
```

```javascript
// This function takes a component...
function withSubscription(WrappedComponent, selectData) {
  // ...and returns another component...
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(DataSource, props)
      };
    }

    componentDidMount() {
      // ... that takes care of the subscription...
      DataSource.addChangeListener(this.handleChange);
    }

    componentWillUnmount() {
      DataSource.removeChangeListener(this.handleChange);
    }

    handleChange() {
      this.setState({
        data: selectData(DataSource, this.props)
      });
    }

    render() {
      // ... and renders the wrapped component with the fresh data!
      // Notice that we pass through any additional props
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
}
```



## Hooks (New) React 16.8+

--- 
See: [Hooks at a Glance](https://reactjs.org/docs/hooks-overview.html)
Rules of Hooks

Hooks are JavaScript functions, but they impose two additional rules:  
- Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.
- Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions.


### Hooks API 
Also see: [Hooks FAQ](https://reactjs.org/docs/hooks-faq.html)




#### Basic Hooks

| Hook                         | Description                               |
| ---------------------------- | ----------------------------------------- |
| `useState`_(initialState)_   |                                           |
| `useEffect`_(() => { ... })_ |                                           |
| `useContext`_(MyContext)_    | value returned from `React.createContext` |

Full details: [Basic Hooks](https://reactjs.org/docs/hooks-reference.html#basic-hooks)

#### Additional Hooks

| Hook                                         | Description                                                                 |
| -------------------------------------------- | ---------------------------------------------------------------------------- |
| `useReducer`_(reducer, initialArg, init)_    |                                                                              |
| `useCallback`_(() => { ... })_               |                                                                              |
| `useMemo`_(() => { ... })_                   |                                                                              |
| `useRef`_(initialValue)_                     |                                                                              |
| `useImperativeHandle`_(ref, () => { ... })_  |                                                                              |
| `useLayoutEffect`                            | identical to `useEffect`, but it fires synchronously after all DOM mutations |
| `useDebugValue`_(value)_                     | display a label for custom hooks in React DevTools                           |

Full details: [Additional Hooks](https://reactjs.org/docs/hooks-reference.html#additional-hooks)




### State Hook

```jsx
import React, {useState} from 'React/React';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  
  return (
          <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
          </div>
  );
}
```
 

 


 

### Effect hook
`useEffect` Hook is an alternative for  `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.

By default, React runs the effects after every render — including the first render.

```jsx
import React, {useState, useEffect} from 'React/React';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
          <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
              Click me
            </button>
          </div>
  );
}
```
 
### Cleaning Up Side Effects
> alternative for componentWillUnmount life cycle method

If you return a function from the side effect inside useEffect then that function will be run every time the side effect is re-ran. Cleanup is run directly before the side effect is run as long as the side effect has occurred at least once.

- return() called every time component unmounts
```javascript
useEffect(()=>{
  ...
  return()=>{
    ...
  }
}, [url]);
```


## useMemo
> Memoization is a caching.
> 
> 
### Building your own hooks
See: [Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)

Custom Hooks are more of a convention than a feature.    
- <b>If a function’s name starts with ”use” and it calls other Hooks, we say it is a custom Hook.</b>

Effects may also optionally specify how to “clean up” after them by returning a function.


```javascript
import React, {useState, useEffect} from 'React/React';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}

- - -  - - - - - - - - - - - - - - - - - - - - - - - -
//Usage
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
          <li style={{ color: isOnline ? 'green' : 'black' }}>
            {props.friend.name}
          </li>
  );
}
```
 


 








## DOM nodes

---
 

### Refs (References)
See: [Refs and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)
Allows access to DOM nodes. 

```jsx
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
        this.myRef = React.createRef();  
    }
    render() {
        const node = this.myRef.current; //access
        
        return <div ref={this.myRef} />;  }
}
```

```javascript
//Hooks
function CustomTextInput(props) {
  const textInput = useRef(null);  
  
  function handleClick() {
    textInput.current.focus();  
  }

  return (<input type="text" ref={textInput}   onClick={handleClick} />);
}
```



### DOM Events
See: [Events](https://reactjs.org/docs/events.html)  
Pass functions to attributes like `onChange`.

```jsx
class MyComponent extends Component {
  render () {
    <input type="text"
        value={this.state.value}
        onChange={event => this.onChange(event)} />
  }

  onChange (event) {
    this.setState({ value: event.target.value })
  }
}
```
 





## Other features

### Transferring props
See [Transferring props](http://facebook.github.io/react/docs/transferring-props.html)

```javascript
//Propagates src="..." down to the sub-component.
class VideoPlayer extends Component {
  render () {
    return <VideoEmbed {...this.props} />
  }
}
- - - - - - - - - - - - - - - - - - - 
<VideoPlayer src="video.mp4" />
```
 




### Top-level API
See: [React top-level API](https://reactjs.org/docs/react-api.html)

```javascript
React.createClass({ ... })
React.isValidElement(c)
```

```jsx
ReactDOM.render(<Component />, domnode, [callback])
ReactDOM.unmountComponentAtNode(domnode)
```

```jsx
ReactDOMServer.renderToString(<Component />)
ReactDOMServer.renderToStaticMarkup(<Component />)
```

There are more, but these are most common.


## JSX patterns   

---
 

### Style shorthand
```jsx
return <div style={{ margin: 0, padding: 0 }}></div>
```

 
### Inner HTML
See: [Dangerously set innerHTML](https://reactjs.org/tips/dangerously-set-inner-html.html)   
```jsx
function markdownify() { return "<p>...</p>"; }
<div dangerouslySetInnerHTML={{__html: markdownify()}} />
```


### Lists

```jsx
//Always supply a `key` property.
class TodoList extends Component {
  render () {
    const { items } = this.props

    return <ul>
      {items.map(item =><TodoItem item={item} key={item.key} />)}
    </ul>
  }
}
```
 



### Conditionals
```jsx
<Fragment>
  {showMyComponent ? <MyComponent /> : <OtherComponent />}
</Fragment>
```

### Short-circuit evaluation
```jsx
<Fragment>
  {showPopup && <Popup />}
</Fragment>
```

New features
------------
 

### Returning multiple elements

You can return multiple elements as arrays or fragments.

#### Arrays

```js
render () {
  // Don't forget the keys!
  return [
    <li key="A">First item</li>,
    <li key="B">Second item</li>
  ]
}
```
 
 
### Returning strings
See: [Fragments and strings](https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-render-return-types-fragments-and-strings)

```js
render() {
  return 'Look ma, no spans!';
}
```


### Errors
See: [Error handling in React 16](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html)   
Catch errors via `componentDidCatch`. (React 16+)
```js
class MyComponent extends Component {
  ···
  componentDidCatch (error, info) {
    this.setState({ error })
  }
}
```
 




### Portals
This renders `this.props.children` into any location in the DOM.   
See: [Portals](https://reactjs.org/docs/portals.html)

```js
render () {
  return React.createPortal(
    this.props.children,
    document.getElementById('menu')
  )
}
```
 


### Hydration
See: [Hydrate](https://reactjs.org/docs/react-dom.html#hydrate)   
Use `ReactDOM.hydrate` instead of using `ReactDOM.render` if you're rendering over the output of [ReactDOMServer](https://reactjs.org/docs/react-dom-server.html).

```js
const el = document.getElementById('app')
ReactDOM.hydrate(<App />, el)
```




## Property validation

---
 

### PropTypes
See: [Typechecking with PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)

```js
import PropTypes from 'prop-types'
```
 


| `any`                     | Anything                             |
|---------------------------|--------------------------------------|
#### Basic

| `string`                  |                                      |
|---------------------------|--------------------------------------|
| `number`                  |                                      |
| `func`                    | Function                             |
| `bool`                    | True or false                        |

 

|Enum ||
|---------------------------|--------------------------------------|
| `oneOf`_(any)_            | Enum types                           |
|---------------------------|--------------------------------------|
| `oneOfType`_(type array)_ | Union                                |

 

|Array ||
|---------------------------|--------------------------------------|
| `array`                   |                                      |
| `arrayOf`_(...)_          |                                      |

 
|Object ||
|---------------------------|--------------------------------------|
| `object`                  |                                      |
| `objectOf`_(...)_         | Object with values of a certain type |
| `instanceOf`_(...)_       | Instance of a class                  |
| `shape`_(...)_            |                                      |

 

|Elements ||
|---------------------------|--------------------------------------|
| `element`                 | React element                        |
| `node`                    | DOM node                             |

 
|Required ||
|---------------------------|--------------------------------------|
| `(···).isRequired`        | Required                             |

### Basic types

```jsx
MyComponent.propTypes = {
  email:      PropTypes.string,
  seats:      PropTypes.number,
  callback:   PropTypes.func,
  isClosed:   PropTypes.bool,
  any:        PropTypes.any
}
```

### Required types

```jsx
MyCo.propTypes = {
  name:  PropTypes.string.isRequired
}
```

### Elements

```jsx
MyCo.propTypes = {
  // React element
  element: PropTypes.element,

  // num, string, element, or an array of those
  node: PropTypes.node
}
```

### Enumerables (oneOf)

```jsx
MyCo.propTypes = {
  direction: PropTypes.oneOf([
    'left', 'right'
  ])
}
```

### Arrays and objects

```jsx
MyCo.propTypes = {
  list: PropTypes.array,
  ages: PropTypes.arrayOf(PropTypes.number),
  user: PropTypes.object,
  user: PropTypes.objectOf(PropTypes.number),
  message: PropTypes.instanceOf(Message)
}
```

```jsx
MyCo.propTypes = {
  user: PropTypes.shape({
    name: PropTypes.string,
    age:  PropTypes.number
  })
}
```

Use `.array[Of]`, `.object[Of]`, `.instanceOf`, `.shape`.

### Custom validation

```jsx
MyCo.propTypes = {
  customProp: (props, key, componentName) => {
    if (!/matchme/.test(props[key])) {
      return new Error('Validation failed!')
    }
  }
}
```

Also see
--------

* [React website](https://reactjs.org) _(reactjs.org)_
* [React cheatsheet](https://reactcheatsheet.com/) _(reactcheatsheet.com)_
* [Awesome React](https://github.com/enaqx/awesome-react) _(github.com)_
* [React v0.14 cheatsheet](react@0.14) _Legacy version_
