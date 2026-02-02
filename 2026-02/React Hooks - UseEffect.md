React Hooks are plain javascript functions that tap into React state and lifecycle features from function components.

There is a number of built-in hooks provided by React to handle common tasks, the most common are:
 - `useState`is the most common hook, used to add local state to a component. 
 - `useEffect` handles side effects like http requests, subscriptions and manual DOM changes. It literally synchronizes the component with an external system (such as a server).
 - `useContext` is used to subscribe to the React Context, so that data can be passed around the component tree without nesting (otherwise, to pass data from parents to children, it would be transmitted through props down the tree).
 - `useRef` creates a persistent reference to a DOM element that doesn't trigger a rerender when it is changed.
 - `useMemo` is used for caching expensive calculations (AKA `memoizing`).

## UseEffect

Among the default use cases suggested by the docs, there are:
 - control a non-react component based on the React state
 - set up a server connection
 - send an analytics log when a component appears on the screen
 - `effects`let you run some code after rendering so that you can synchronize your component with some system outside of React.

There's 2 types of logic in a React component:
 - Rendering code: this must be pure, it returns the `JSX`  that gets painted on the screen. The keyword here is `calculate`. The view is `calculated` as a result.
 - Event handlers: these are functions inside of components that _do things_. Event handlers contain _side effects_ as they change the state of the app, caused by a specific action.

Effects let us specify side effects caused by the app action of rendering itself.

## When do Effects run?

By default, Effects run after every commit. In React, a commit is a phase of the UI update process.
