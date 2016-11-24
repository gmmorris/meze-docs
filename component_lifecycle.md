# Component Lifecycle

Meze allows you to hook into various lifecycle events of components in a composition. Inspired by [Inferno](https://github.com/trueadm/inferno)'s Hook system, we allow both the component developer to hook into these events via DefaultProps and any developer using the component via regular props.

Below is the table of the various events you can hook into.

| Name                      | Triggered when                                                 | Arguments to callback           |
| -----------               | --------------                                                 | -----------------------         |
| `onCreated`               | a DOM node has just been created                               | `domNode`                       |
| `onAttached`              | a DOM node being attached to the document                      | `domNode`                       |
| `onWillDetach`            | a DOM node is about to be removed from the document            | `domNode`                       |
| `onWillUpdate`            | a DOM node is about to perform any potential updates           | `domNode`                       |
| `onDidUpdate`             | a DOM node has performed any potential updates                 | `domNode`                       |
| `onComponentWillMount`    | a stateless component is about to mount                        | `domNode, props`                |
| `onComponentDidMount`     | a stateless component has mounted successfully                 | `domNode, props`                |
| `onComponentWillUnmount`  | a stateless component is about to be unmounted                 | `domNode, props`                |
| `onComponentShouldUpdate` | a stateless component has been triggered to updated            | `domNode, lastProps, nextProps` |
| `onComponentWillUpdate`   | a stateless component is about to perform an update            | `domNode, lastProps, nextProps` |
| `onComponentDidUpdate`    | a stateless component has performed an updated                 | `domNode, props`                |

### Using hooks

It's simple to implicitly assign hooks to both DOM nodes and stateless components.
Please note: stateful components (ES2015 classes) from `inferno-component` **do not** support hooks.

```javascript
function createdCallback(domNode, props) {
    // [domNode] will be available for DOM nodes and components (if the component has mounted to the DOM)
	// [props] will only be passed for stateless components
}

InfernoDOM.render(<div onCreated={ createdCallback } />, document.body);

function StatelessComponent({ props }) {
	return <div>Hello world</div>;
}

InfernoDOM.render(<StatelessComponent onComponentWillMount={ createdCallback } />, document.body);
```

Hooks provide powerful lifecycle events to stateless components, allowing you to build components without being forced to use ES2015 classes.
