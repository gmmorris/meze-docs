# Thinking in Components

Components let you split your application into independent, reusable pieces, and think about each piece in isolation.

In essence, components are simple functions, referred to as Constructor functions. They accept a two arguments, **props** and **context**, which are a plain Javascript Objects, and return either an object or primitive which are passed back to whoever composed them.

## Basic API
Meze Components is designed to work as closely to React Components as possible, so the API should be familiar to anyone who has worked with React,  but there are several nuances which are different.

### props
The props object, is a plain Javascript object, which will always get passed into you Component's constructor function.

```js
import Meze from 'meze'

const GetPersonalisedMessage = (props) => {
  return `Hello ${props.name}, we're speaking via composition`
}

Meze
  .compose(<GetPersonalisedMessage name="Hummus" />)
  .then(result => {
    console.log(result)
  })

```


