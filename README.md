# Meze



***Meze***, a word with its roots in antiquity, describes a selection of small dishes served accompanying alcoholic drinks, whose purpose is three-fold: to complement and enhance the taste of the drink, to provide the backdrop for a social gathering and to decouple the implementation of the individual dishes so that they may be consumed by the hungry developer in whichever way suits them the best.

The above is as true for real life *Meze* as for it's Javascript counterpart.

Born out of a thought experiment, *Meze* provides the Component Composition API popularized by the *React* library in order to declaratively compose a process. *Meze* is designed to make it painless to express complex operations while striving for the simplicity of functional composition.

## Key Features
* Stateless Components maintain the standard React API, with slight changes to better reflect their purpose as implementations of data & process ,rather than stateful UI
* Meze.compose mounts a component tree which reduces down to a single return value
* Asynchronous processes are seemlessly supported via a Promise based API between composed component trees
* Fully supports JSX in order to make adoption as seemless as possible for developers already used to the syntax and developer experience of React

