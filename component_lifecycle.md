# Component Lifecycle

Meze allows you to hook into various lifecycle events of components in a composition. Inspired by [Inferno](https://github.com/trueadm/inferno)'s Hook system, we allow both the component developer to hook into these events via DefaultProps and any developer using the component via regular props.

Below is the table of the various events you can hook into.

| Event name | When is the event called? | Arguments |
| ---------- | -------------- | ----------------------- |
| `componentWillMount` | a component is about to mount ||
| `componentDidMount` | a component has mounted successfully, has been composed and has its resulting composition is at hand | `composition` |
| `componentWillUnmount` | a component is about to be unmounted and its resulting composition returned to the parent component | `composition` |
| `componentFailedMount` | a component has failed to mount and has resulted in an exception | `exception` |

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
