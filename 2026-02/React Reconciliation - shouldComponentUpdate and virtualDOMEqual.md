Reconciliation in React is the process of updating the DOM to match the component tree with the current state of each component. It helps update the painted UI efficiently and it is an algorithm based on Fiber architecture, that allows the work to be broken down into smaller units to be paused and resumed. This is a core concept of React as it prevents blocking the main execution thread, resulting in a smooth user experience.

When deciding whether to repaint or not a component after a Render and Commit cycle has been triggered, React uses 2 main functions in order to decide which component functions to call and which to skip (and keep as-is, to save the resource intensive effort of repainting).

These 2 functions are:
 - `shouldComponentUpdate` : A lifecycle function that is triggered before the re-rendering process starts. The default implementation of this function returns `true`, but a developer can return `false` instead, to skip the whole rendering process (that includes calling `render` on the current component and the ones below).
 - `vDOMEq` = `virtualDomEqual`: React maintains an internal representation of the rendered UI called the _virtual DOM_ . This is useful to avoid creating and accessing DOM nodes beyond necessity. When a component's **props or state** change, React decides whether an actual DOM update is necessary by comparing the new element with the one from the previous render.

There are important rules to how these 2 functions work in the process of a component rerender:
 - Both of these 2 functions need to return `true` for a given component to get it to rerender.
 - `shouldComponentUpdate`is always evaluated fist before running `vDOMEq` and it acts as a short circuit: when `shouldComponentUpdate`returns `false`, `vDOMEq`is not even evaluated.

Lastly, there are 3 ways to make sure that we are avoiding reconciliation when a parent component has triggered a render cycle but our target component has no props changed:
 - The legacy way, for class components, inherit from `React.PureComponent`:
	 - Guarantees that a shallow comparison is used to evaluate `shouldComponentUpdate`.
	 - Complex data structure changes won't trigger render cycles.
- The _memoization_ way, for function components, wrap the component in `memo`:
	- Guarantees that the `memoized` version of the component will not rerender when its parent rerenders as long as its props have not changed. 
- The *ReactCompiler* way:
	- Guarantees that all components are evaluated as if they were wrapped with `memo` at build time.
	- Even better than `memo` as it avoids bugs that would break `memo` , like using an arrow function as an event handler in a component (an arrow function generates a brand new function every time the component is evaluated, rendering `memo` useless even if the props never change).

Sources used: 
 - `shouldComponentUpdate`: https://legacy.reactjs.org/docs/optimizing-performance.html#shouldcomponentupdate-in-action
 - `ReactCompiler`