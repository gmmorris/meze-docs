# Children
## Contents of Children
Whenever a component constructor executed, Meze will check whether the current instance has been composed with any child components and if so add a *children* prop to the *props* argument.
Just like React, children is the only property added to the *props* by Meze itself and if no child components or values are composed with the component, it will be omitted entirely.

The value of the children prop is a Meze specific data structure designed to make it easier to interact with the list of children.

A common mistake made by developers is to assume that the *children* property will contain only Component Instances but it will in fact contain any child values that the component is composed with.
```js
const Echo = ({ children }) => {
  /*
  The `children` prop will contain three
  values:
    [0] The string `You know nothing`
    [1] A Component Instance of the EchoName with the props { name: "John"}
    [2] A Component Instance of the EchoName with the props { name: "Snow"}
  */
}

compose(
  <Echo>
    You know nothing
    <EchoName name="John" />
    <EchoName name="Snow" />
  </Echo>
).then(console.log)
```

## Manipulating Children
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

## Children API reference

Each of the following functions resides on the **Meze.Children** object and they can be split into two groups: Pre and Post composition.
Pre composition are operations which are applied to Component Instanced *before* they are mounted, and Post composition are operations which are applied to the return values of the child components.

### Pre Composition

#### map(children : Children | [], mapper : (item, index) => any) => Children
The map() function creates a new Children data structure with the results of calling a provided function on every element in this children data structure.
Note that if a child is a component then it will still, at this point, be an unmounted Component Instance.

If no mapper function is provided then *map* uses the *identity* function, which would essentially mean a no-op, but hey, maybe some developers roll that way, no criticism here.

#### mapToArray(children : Children | [], mapper : (item, index) => any) => []
The mapToArray() function operates precisely like map() except that the return value will be an Array.

#### forEach(children : Children | [], mapper(item, index) => any)
The forEach() method executes a provided function once per element in the Children data structure.

#### cloneWithProps(children : Children | [], props : Object | () => Object) => Children

#### reduce(children : Children | [], reducer : (reduciton, item, index) => any, initialValue) => any

  
#### only(children : Children | []) => any

### Post Composition

#### reduceComposed(children : Children | [], reducer : (reduciton, item, index) => any, initialValue, context) => any
#### mapComposed(children : Children | [], mapper : (item, index) => [], context) => any

#### onlyComposed(children : Children | [], context) => any
