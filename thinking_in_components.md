# Thinking in Components

Components let you split your application into independent, reusable pieces, and think about each piece in isolation.

In essence, components are simple functions, referred to as **constructors**. They accept a two arguments, **props** and **context**, which are a plain Javascript Objects, and return either an object or primitive which are passed back to whoever composed them.

## Basic API
Meze Components is designed to work as closely to React Components as possible, so the API should be familiar to anyone who has worked with React,  but there are several nuances which are different.

### Component & the constructor function
The constructor function is called once for every instance of the Component, and should ideally be a *pure* function, meaning it only refers to the *props* and *context* it has been handed and returns a value rather than cause side effects outside of its scope by referencing global state.

Defning a constructor function is simple. Any function can act as a constructor as long as it maintains the API by accepting a single *props* argument, or at the most the second *context* argument.

For example, the following functions may all be used as constructors:
```js
function hasProps(props) {
  return Object.keys(props).length > 0
}

function echo({ value }) {
  return value
}

function fetch({ getTimeoutURL }) {
  return fetch(getTimeoutURL)
    .then(timeout => new Promise(resolve => {
      setTimeout(resolve, timeout)
    }))
}

```

In order to turn a constructor into a *Component* though, you still need to pass the constructor to the Component factory.
```js
import { Component } from 'meze'

function hasProps(props) {
  return Object.keys(props).length > 0
}

const HasPropsComponent = Component(hasProps)
```

But you will very rarely need to actually use the *Component* factory, because as long as you name you function in the **uppercase** (this is a JSX syntax requirment), our *compose* function will turn every function into a Component for you.
This means that when you use a plain function within a Meze composition, all you have to do is drop the function into a composition and Meze will do the rest.
```js
import { Component } from 'meze'

// Note the usage of Uppercase 'hasProps' becomes 'HasProps'
function HasProps(props) {
  return Object.keys(props).length > 0
}

Meze.compose(<HasProps name="Hummus" />)
```

### props
The props object, is a plain Javascript object, which will always get passed into you Component's constructor.
Which ever properties are defined on the component when it's composed, will be passed as properties of this object.
Just like React, the only property added to the *props* by Meze itself is the optional *children* prop.
The children prop, described in detail in it's own chapter, is a special Data Structure and acts as a wrapper for all child components with which the current component has been composed.

```js
import Meze from 'meze'

const MyComponent = (props) => {
  /*
    props is now an object with three props:
    {
      left: 0,
      right: 1,
      children : ChildrenDtataStructure(
        [
          <FirstChild />,
          <SecondChild />
        ]
      )
    } 
  */
}

Meze.compose(
  <MyComponent left={0} right={1}>
    <FirstChild />
    <SecondChild />
  </MyComponent>
 )

```

### context
The true power of the Component Composition implemented by Meze comes from the unidirectional flow of data between your components and the predictability of a component's behavior based on the value of its props. 

Sometime, though, you may want to simplify your API by defining a Context for your current composition tree.
This can be useful when composing a set of components who all refer to a single source of (ideally) read only data, and you wish to avoid having to manually pass this source of data down through all the props.

In general we would recommend avoiding context where possible, but we chose to provide this API as we find it becomes an invaluable feature when used correctly.

The *context* as passed into every constructor as its second argument and is a plain Javascript object.

The *context* is set by the *compose* function.

```js
import Meze from 'meze'

const ChildComponent = (props, context) => {
  return context.message
}

const ComponentWithContext = (props, context) => {
  return <ChildComponent />
}

Meze.compose(
  <ComponentWithContext />,
  {
    message: 'This is a value on the context, it will get logged'
  }
 )
 .then(result => {
   console.log(result)
 })

```

### return values
In React a Component is expected to return an Element, which makes sense for React as it is used to compose a tree of Elements.
Meze, on the other hand, has a very different purpose which is to compose data and execute a process, hence the return values in a Meze Component can be varied.

#### primitives
A Meze component may return any Javascript primitive, which includes the following: string, number, boolean, null, undefined and symbol.
All are valid return values and it is up to the parent component to deal know how to process the returned value.

### objects and arrays
A Meze component may return a variety of Objects, but the way in which Meze treats them can change depending on the type.
When a Component provides a plain Javascript object or an Array as its return value, Meze will pass it to the parent component, just like a promitive, but it will also scan the object/array for all internal components and mount them as well.

```js
import Meze from 'meze'

let counter = 0
const ChildComponent = () => {
  return ++counter
}

const ComponentWithChildren = () => {
  return {
    child: <ChildComponent />,
    arrayOfChildren: [
      <ChildComponent />,
      {
        child: <ChildComponent />
      }
    ]
  }
}

Meze.compose(
  <ComponentWithChildren />
 )
 .then(result => {
   console.log(result)
 })

```
In the above snippet all child components will be composed by Meze, resulting in the following output:
> { child: 1, arrayOfChildren: [ 2, { child: 3 } ] }

