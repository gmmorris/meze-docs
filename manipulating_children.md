# Manipulating Children

Whenever a component constructor is called, Meze will check whether the current instance has been composed with any child components and if so add a *children* prop to the *props* argument.
This value of the children prop is a Meze specific data structure designed to make it easier to interact with the list of children.

All of the following manipulation functions are completely stand alone and receive your *children* prop as a first argument, so you can access them via the *Meze.Children* object, or use a direct reference to them.

Both of the following components will behave exactly the same.
```js
import Meze from 'meze
const {mapToArray } = Meze.Children

const Summarize = function (props) {
  return {
    contents: Meze.Children.mapToArray(props.children)
  }
}

const SummarizeV2 = function (props) {
  return {
    contents: mapToArray(props.children)
  }
}
```

## Children API reference

Each of the following sit on the **Meze.Children** object.
#### mapToArray(children : Children | [], mapper : (item, index) => any) : []

### map(children : Children | [], mapper : (item, index) => any) : Children

### forEach(children : Children | [], mapper : (item, index) => any)

### reduce(children : Children | [], reducer : (reduciton, item, index) => any, initialValue) : any
###
###
###