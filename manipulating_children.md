# Manipulating Children

Whenever a component constructor is called, Meze will check whether the current instance has been composed with any child components and if so add a *children* prop to the *props* argument.
This value of the children prop is a Meze specific data structure designed to make it easier to interact with the list of children.

All of the following manipulation functions are completely stand alone and receive your *children* prop as a first argument, so you can access them via the *Meze.Children* object, or use a direct reference to them.

Both of the following components will behave exactly the same.
```js
import Meze from 'meze
const { mapToArray } = Meze.Children

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

## Contents of Children

## Children API reference

Each of the following functions resides on the **Meze.Children** object and they can be split into two groups: Pre and Post composition.
Pre composition are operations which are applied to Component Instanced *before* they are mounted, and Post composition are operations which are applied to the return values of the child components.

### Pre Composition

#### mapToArray(children : Children | [], mapper : (item, index) => any) => []
The map() method creates a new array with the results of calling a provided function on every element in this array.

#### map(children : Children | [], mapper : (item, index) => any) => Children

#### forEach(children : Children | [], mapper(item, index) => any)

#### cloneWithProps(children : Children | [], props : Object | () => Object) => Children

#### reduce(children : Children | [], reducer : (reduciton, item, index) => any, initialValue) => any

  
#### only(children : Children | []) => any

### Post Composition

#### reduceComposed(children : Children | [], reducer : (reduciton, item, index) => any, initialValue, context) => any

#### onlyComposed(children : Children | [], context) => any
