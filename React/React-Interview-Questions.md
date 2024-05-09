# React Interview Questions

**_What is JSX:_** Javascript with XML, syntactic sugar to make javascript look like HTML. Syntactic sugar over create.reactElement, the JSX will get reconfigured under the hood to basic javascript

**_Why is Class Classname in React:_** Class is a reserved keyword in javascript. Under the hood bable is doing the translation into javascript

**_Describe Dataflow in React_**:

Dataflow is unidirectional: meaning all components in react have a parent child relationship, and we pass data "down" from the parents to the children.

- theres things like forward ref and useImperativeHandle to allow a parent to call a function thats defined in a child
- theres methods of global state management to avoid too much prop drilling (React Context, Redux, Zustand)
  How would you delay an API call until a component is mounted:
- In a functional component useEffect, with no dependencies in the second argument, would result in the code inside running once the component is mounted. Its possible to use the useEffect hook to replicate other lifecycle methods as well in a functional component
- In a class component, we could use component.DidMount(), which is just one of the other lifecycle methods

**_What are the lifecycles:_**

- component did mount
- component did update
- componenet did unmount

**_Should you use ternaries or the and operator:_**

- depends on the situation if its outside of the render
- javascript reads the falsey and doesnt compute the right side of the operator, which if there was code to do something if the value was false and you wanted to respond to that computation in the code to the right of the operator, it would not be picked up on execution
- I avoid using it inside the render block because there was a bug for a while that resulted in 0s being shown when the left side of the operator resulted in falsey
  What is binding: Data binding is the coupling and synchronization of two data sources

**_What is Higher Order Component:_**

- a function that takes a component as an argument and returns a new component that wraps the original component.
- They allow you to reuse component logic across multiple components.

**_What is create-react-app:_**

- a cli for creating a new react app
- tools are preconfigured when using the cli and you can use templates to configure different dependencies like typescript

**Redux:** dependency for storing global state variables as a javascript object

**_Events:_** application user interactions (hovering, key on keyboard, onClick)

**_SyntheticEvents:_** a wrapper based on browser's native events. prevents browser inconsistencies, and ensures that the event works across multiple platforms.

**_Stateful components:_** store the state changes that happen to them in memory
