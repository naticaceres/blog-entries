React uses a three step process to paint the UI elements and deciding when and how to repaint them with changes.
These steps are:
  1) **Trigger** a render: The action that fires a repaint. 
  2) **Render** the component: Interpret the `jsx` into language that the browser can paint, in the right state.
  3) **Commit** to the `DOM` : The virtual DOM reconciliation.

## 1) Trigger a render.
There are 2 to ways a component can get rendered:
 - It is the first time a component will ever be rendered: **Initial render**.
	 - This is triggered in cascade by the `root.render` statement in your React app `index.js`.
 - The **state** of the component or the state of one of its ancestors has been **updated**.
	 - After the initial render, invoking the `set function` of the component automatically queues a rerender.

## 2) Render the component.
As React components are none other than javascript functions, a rerender is in fact React calling the components that need to be repainted.
 - On an **initial render**:
	 - React calls the **root** component. 
	 - React **creates** the DOM nodes for each of the HTML tags returned by each component function.
 - For **state updates** of individual components:
	 - React calls the **function component** that triggered the render.
	 - React **calculates** which of the component properties have changed since the last render.
The interesting catch here is that the **render process is recursive**. When the updated component returns a nested component, React will call the nested component function, and so on until there's no more nested component functions to call.

## 3) Commit to the DOM.
Only after all the components that have to be repainted have been called (AKA Rendered), React modifies the DOM.
 - In the **initial render**, all the DOM nodes created are put on the screen using the native `appendChild()` method of the document.
 - In rerenders, React applies the minimal necessary operations, that were calculated during the rerender step, to get the DOM to match the latest render output.

React only changes the DOM nodes when there's a difference between renders. When there are no differences, the components are left untouched.

## 4) Browser paint.
When the rendering is complete and the DOM is updated by react, then the browser repaints the screen. This last step is formally known as the browser rendering or painting, AKA actually displaying the updated app on the screen.