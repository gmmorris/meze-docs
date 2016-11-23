# Thinking in Components

Components let you split your application into independent, reusable pieces, and think about each piece in isolation.

In essence, components are nothing more than functions. They accept a single argument, named **props**, which is a plain Javascript Object, and return either an object or primitive which are passed back to whoever composed them.



## A Simple Component
Meze only supports Stateless Component, as we want to encourage pure stateless operations. Just as with React, the usage of JSX is optional, but we find its usage makes it easier for React developers to reason about Meze code.

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


