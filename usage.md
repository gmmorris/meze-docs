# Basic Usage

If you have experience using React then you should feel comfortable jumping right into Meze.

## A Simple Component
Meze only supports Stateless Component, as we want to encourage pure stateless operations. Just as with React, the usage of JSX is optional, but we find it's usage makes it easier for React developers to reason about Meze code.

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

Note how the API of the *Meze.compose* method is that it takes a single component instance and returns a promise. All component trees start at a single root component, just like React, but the resolution is assumed to be asynchronous hence the main interaction with the library is via Promises.
Suffice to say we're very pleased about Promises becoming an official Javascript primitive, elevating it's usage to what we consider ubiquitous.

## A Composition of Components


