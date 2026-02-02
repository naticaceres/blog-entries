React Hooks are plain javascript functions that hook 
according to the official `react.dev` documentation: 
> The `useEffect` hook, lets you synchronize a component with an external system

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
