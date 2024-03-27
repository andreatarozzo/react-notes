# Introduction

These are some React notes I took when I started working on React and had laying around. <br>
I decided to publish these because they might be useful for anyone approaching React for the first time or just for a quick knowledge refresh on a specific topic.

If even just one person will find this useful I'll be happy 😬.

Also, please, if you find something that is not correct open a PR/reach out 🙏.

# Table of Contents

- [What is React](#what-is-react)
  - [Why React is said to be Declarative and not Imperative?](#why-react-is-said-to-be-declarative-and-not-imperative)
  - [What is a React Component ?](#what-is-a-react-component-)
    - [React Components Vs. HTML elements](#react-components-vs-html-elements)
    - [Functional Components Vs. Class Components](#functional-components-vs-class-components)
    - [How can I access the state and lifecycle of a React Component?](#how-can-i-access-the-state-and-lifecycle-of-a-react-component)
  - [What is a React Element ?](#what-is-a-react-element-)
  - [What is a React Component Instance ?](#what-is-a-react-component-instance-)
  - [What is the Virtual DOM in React ?](#what-is-the-virtual-dom-in-react-)
    - [What if a component changes and the virtual DOM needs to be updated ?](#what-if-a-component-changes-and-the-virtual-dom-needs-to-be-updated-)
  - [React Renderes and the actual rendering phase](#react-renderes-and-the-actual-rendering-phase)
    - [How React communicates with the renderes?](#how-react-communicates-with-the-renderes)
    - [React Fiber's main phases](#react-fibers-main-phases)
      - [Render Phase (asynchronous execution)](#render-phase-asynchronous-execution)
      - [Commit Phase (synchronous execution)](#commit-phase-synchronous-execution)
  - [Fibers - React Reconciler's unit of work](#fibers---react-reconcilers-unit-of-work)
    - [Fiber structure](#fiber-structure)
  - [The Fibers tree](#the-fibers-tree)
    - [What is an Effect?](#what-is-an-effect)
  - [What are React Hooks?](#what-are-react-hooks)
    - [useState](#usestate)
      - [Updating Objects in state](#updating-objects-in-state)
    - [useEffect](#useeffect)
      - [When to avoid using the useEffect hook?](#when-to-avoid-using-the-useeffect-hook)
      - [When we want to use the useEffect hook?](#when-we-want-to-use-the-useeffect-hook)
      - [How to use the useEffect hook](#how-to-use-the-useeffect-hook)
        - [useEffect hook dependant on every state/prop change](#useeffect-hook-dependant-on-every-stateprop-change)
        - [useEffect hook dependant on specific state changes/prop changes](#useeffect-hook-dependant-on-specific-state-changesprop-changes)
        - [useEffect hook defined with an empty dependencies array](#useeffect-hook-defined-with-an-empty-dependencies-array)
    - [useLayoutEffect](#uselayouteffect)
    - [useRef](#useref)
      - [Ref Forwarding](#ref-forwarding)
    - [useImperativeHandler](#useimperativehandler)
    - [useContext](#usecontext)
    - [useReducer](#usereducer)
    - [useMemo](#usememo)
    - [useCallback](#usecallback)
    - [useDeferredValue](#usedeferredvalue)
  - [Custom Hooks](#custom-hooks)
  - [Why Hooks cannot be used inside a loop or a condition block ?](#why-hooks-cannot-be-used-inside-a-loop-or-a-condition-block-)
  - [Why using a State Management Library in React ?](#why-using-a-state-management-library-in-react-)
  - [React.memo & Pure Components](#reactmemo--pure-components)
  - [HOC (High-order component)](#hoc-high-order-component)
  - [Error Boundaries in React](#error-boundaries-in-react)
  - [Suspense in React](#suspense-in-react)
    - [Error handling in Suspense](#error-handling-in-suspense)
  - [React.lazy](#reactlazy)
  - [Controlled Vs. Uncontrolled Components](#controlled-vs-uncontrolled-components)
    - [Uncontrolled Components](#uncontrolled-components)
    - [Controlled Components](#controlled-components)
  - [Controlled Vs. Uncontrolled Inputs](#controlled-vs-uncontrolled-inputs)
  - [Where should I store the state of my component?](#where-should-i-store-the-state-of-my-component)
  - [Compound Component](#compound-component)
  - [Cloning a Component](#cloning-a-component)
  - [React project folder structure](#react-project-folder-structure)
- [React router](#react-router)
  - [Simple React router implementation](#simple-react-router-implementation)
  - [Navigation](#navigation)
  - [Nested Routes](#nested-routes)
    - [Outlet Context](#outlet-context)
    - [Global Layout](#global-layout)
  - [Dynamic Routes](#dynamic-routes)
  - [useNavigate React Router Hook](#usenavigate-react-router-hook)
  - [Loaders](#loaders)
  - [Error handling with React Router](#error-handling-with-react-router)
    - [Error handling with Async React Router](#error-handling-with-async-react-router)
  - [Lazy Loading with React router](#lazy-loading-with-react-router)

<br><br>

# What is React

React.js is an open-source JavaScript library, provided by Facebook, for building user interfaces.

<br>

## Why React is said to be Declarative and not Imperative?

React is said to be declarative because through the react’s code we declare what the UI should look like depending on the state of the application (declarative) but we don’t describe exactly what steps react should take in order to be able to display a specific state of the application (imperative).

For example, if we have a door and we would like to have it painted white, we would declare to the carpenter that “We want the door painted white” while we don’t say “We want the door sanded using 180 grain sandpaper, then placed in horizontally in a flat surface, then you should take the white paintbrush and dip it in the color tin, …

The declarative approach used by react has several advantages such as:

- Easier to understand an dd use
- Easier to maintain
- Better performance because react can handle the optimization of the app rendering process

<br>

```TSX
// React - Declarative
export const MyComponent: FC<MyComponentProps> = (props) => {
  return (
    <div>
      <h1>My Component</h1>
      <p>This is a paragraph</p>
    </div>
  );
}

// Standard JS DOM manipulation - Imperative
export const generateNewElement = (): Node => {
  // We need to explicitly define and create each single element
  const div = window.document.createElement('div');
  const h1 = window.document.createElement('h1');
  const p = window.document.createElement('p');

  // We also need to explicitly assign the text within our new elements...
  h1.textContent = 'My Element';
  p.textContent = 'This is a paragraph';

  // ...and remember to append the elements to the host element
  div.append(h1, p)

  return div;
}
```

<br>

## What is a React Component ?

A react component is a reusable piece of code that can be as simple as a button or complex as an entire page.
React components have props (component inputs), a state and a lifecycle and can be of two different kind:

- Functional Component
- Class Component

In React a component returns/produces a React Components Tree. <br>
Depending on the kind of component the components tree will be either the value returned by the functional component itself in case of functional components, or, the result of the `render()` method for class based components.

```TSX
// Functional Component
export const MyComponent: FC<MyComponentProps> = (props) => {
  return <h1>Hello World</h1>
}

// Class Component
export class MyComponent extends Component {
  render(): ReactNode {
      return <h1>Hello World</h1>
  }
}
```

<br>

### React Components Vs. HTML elements

One of the main differences between an html element and a component is that a component has a lifecycle and a state which react uses to understand when to update it.

Another difference is that react’s components accept props which are basically inputs to the component to dynamically pass some values/state while html elements cannot handle inputs in the same way.

In the end html elements don’t provide the same level of abstraction and reusability that react components provide.

<br>

### Functional Components Vs. Class Components

Class components are the old way of defining components and they provide an easy access to the component state and to predefined methods to access the component lifecycle. <br>
On the other hand functional components cannot do that directly without the use of hooks but they offer a simpler way to implement components.

While class components are tied up to the default set of predefined methods to handle lifecycle and are generally more rigid entities, functional components can be way more flexible even because it is possible to define custom hooks to meet the needs of a specific React application.

Before the introduction of the current default reconciler ( React Fiber ) the performance difference between class and functional component was noticeable and class components were preferred in some scenarios but now this performance gap became less noticeable.

<br>

### How can I access the state and lifecycle of a React Component?

In a <ins>functional component</ins> we can access the state and lifecycle of the component by using react hooks `useState` and `useEffect` while in <ins>class components</ins> we use the `this` keyword to access the `state` property of the class while to access the lifecycle we use predefined methods, such as, `componentDidMount` (after the component mounted) and `componentWillMount` (before che component is mounted).

<br>

## What is a React Element ?

A React element can be described as a plain JS object used by React to describe a component instance/DOM node and its properties.

React elements are the building blocks of a the React Components Tree and they are generated through the method `React.createElement(type, props, children)` which is call by React to convert the `JSX` within the component into its abstracted version.

Before React 17, because React would need to call the `createElement()` method, we would need to explicitly import React when defining a component because of the needed JSX conversion. <br>
From React 17 the necessary functions required to do the conversion of the JSX are imported automatically and so it is not necessary to explicitly import React into component files.

```TSX
// React Element
{
  $$typeof: Symbol(react.element),
  key: 'my-key',
  props: {
    children: [
      {
        $$typeof: Symbol(react.element),
        key: null,
        props: {
          children: 'Text inside h1 element'
        },
        ref: null,
        type: 'h1'
      }
    ]
  },
  ref: null,
  type: 'div'
}

// JSX equivalent
export const MyComponent: FC<MyComponentProps> = () => {
  return (
    <div key='my-key'>
      <h1>Text inside h1 element</h1>
    </div>
  )
}
```

<br>

## What is a React Component Instance ?

When we are rendering a component in JSX using, for example, `<MyComponent />`, React behind the scene will call the component to get its react component instance which is used by React to keep track of the components state and lifecycle.

```TSX
{
  $$typeof: Symbol(react.element),
  key: 'my-key',
  props: {},
  ref: null,
  type: ({ children }) => {...}
}
```

The component instance object structure seems exactly the same as a React element with the only difference in the type property which instead of being a specification of an HTML element ( h1, div, … ) is a function that when called will return a react element.

<br>

## What is the Virtual DOM in React ?

When it's time to render the application React will start from the top component and recursively traverse all the child components in order to generate a tree of elements which is simply a JS object stored in memory called Virtual DOM.

React interacts directly with the Virtual DOM and not with the actual DOM because operation on the real DOM are way more resource/time intensive than operating on a plain JS object (which is why React is quite fast).

When its time to actually updating the real DOM React basically passes the components tree to its renderer ( which will be covered in the next section ).

<br>

### What if a component changes and the virtual DOM needs to be updated ?

Whenever there is a change in a component a new tree is computed and compared with the old one using the `diffing algorithm` so React can find the smallest number of operations required to transform the old tree into the new tree in the DOM.

The `diffing algorithm` allows react to have a number of operations to perform always less than the number of the elements (making it very efficient) in the tree, this is possible because of the two assumptions made by React:

- Two elements with different type will always return a different tree

  ```HTML
  <div>                        <div>
    <h1>My Header</h1>   Vs.     <h2>My Header</h2>
  </div>                       </div>
  ```

  In this first case above, because we have a change of type of element, from `h1` to `h2`, React will rebuild the tree inside the `<div>` element entirely meaning that all components in the tree that are children of the element that changed will be unmounted/destroyed alongside their state.

  ```HTML
  <div className="visible">         <div className="hidden">
    <h1>My Header</h1>        Vs.     <h1>My Header</h1>
  </div>                            </div>
  ```

  In this second case, because the type of the component doesn’t change but the only thing that changes is a `prop value`, React won’t rebuild the tree entirely but it will just update the prop value in the virtual DOM without creating a new component instance.

  <br>

- When dealing with lists of elements each element should use a key property to uniquely identify each element in the list.

  Keys are used by the `diffing algorithm` to identify what changed and what not in a list of elements that React needs to render, so even if we rearrange the order of the element but each element has its key untouched React won’t rebuild the whole tree again for the component.

  This is why we shouldn’t use an index as a key because if, for example, we have a list of things to render and we prepend a new item to the list, despite only 1 item has been changed the whole tree will be re-computed because all keys for all other elements will be different.

  <br>

  <b>An edge case with keys</b>

  Let’s imagine one situation where we have a component which contains a `<Counter />` child component ( which controls its own counter state and includes a buttons to increment/decrement the counter ) and a button to switch from the primary counter to the secondary counter.

  ```TSX
  export const MyComponent: FC<MyComponentProps> = () => {
    const [showPrimaryCounter, setShowPrimaryCounter] = useState(false);

    return <>
      { showPrimaryCounter
        ? <>
            <h1>Primary Counter</h1>
            <Counter />
          </>
        : <>
            <h1>Secondary Counter</h2>
            <Counter />
          </>
      }
      <button onClick={() => setShowPrimaryCounter(!showPrimaryCounter)}>
        Switch Counters
      </button>
    </>
  }
  ```

  In this specific scenario if we play around with the counter by incrementing its value and then we click on the Switch Counters button we would expect to see a different h1 and a counter value that is being reset considering we are rendering a totally different Counter component. <br>
  Unfortunately that is not the case in this specific scenario and if we play around with the counter and the switch we won’t see the counter value being reset. <br>
  This happens because the structure of the react elements tree remains technically unchanged and so React assumes that we are using the same Counter component maintaining also its actual state.

  To avoid situations like this one we can simply add a key property to our component so the diffing algorithm is able to understand that the Counter component actually changed and to not reuse the old one.

<br>

## React Renderers and the actual rendering phase

Renderers are those packages, such as React DOM and React Native, in charge of actually updating the DOM.

React requires this kind of "help" because React itself provides us just the tool to define components alongside using the diffing algorithm to generate the virtual DOM but it doesn't actually have the functionality to update the real DOM.
This is intended to keep react non platform specific.

The renderers takes the virtual DOM and execute a process to actually update the DOM where it needs to be updated.

It is necessary to have a renderer used alongside React because React actually communicates with the renderer using some specific properties and methods.

<br>

### How React communicates with the renderers?

Whenever a new instance of a component is created ( for class component ) an `updater` field is set to by the renderer and that field will be used to push updates to the renderer queue.
With hooks, React holds a property `currentDispatcher` which holds the same renderer reference as the `updater` field.

The updates in the queue are handled one by one by the actual changes to the DOM are handled in one go at the end at the same time.

<br>

## React reconciliation process & React Fiber

React Fiber is the default reconciler used by React since React 16 which handles animations and responsiveness working in an asynchronous fashion. <br>
Its main ability is to split the work in chunks or Fibers ( unit of work ) that can be stopped, resumed, aborted and reused easily, process those units of work and then commit the changes in the actual DOM.

It is a huge upgrade compared to the old reconciler that was working in a synchronous fashion like a stack meaning that some work placed in the stack needed to be completed in order to move to the next task causing performance issues.

<br>

### React Fiber's main phases

#### Render Phase (asynchronous execution)

During this phase the fibers the reconciler computes the fibers and generates a fibers tree.

During this phase React proceeds in prioritizing tasks, pause tasks that don't have the priority or even discard tasks if needed.
During this phase Fibers methods such as beginWork or completeWork are called multiple times.

Within a component some lifecycle methods are called during the render phase such as the `render` method, the `getDerivedStateFromProps` and `shouldComponentUpdate`. <br>
Because the execution of the methods above happen in the Render phase no side effects must happen within the logic of those methods.

#### Commit Phase (synchronous execution)

During this phase the actual changes are applied to the DOM and side effects are triggered. <br>
This phase is synchronous because updates to the DOM need to be completed once started.

One of the lifecycle methods that runs during this phase is the `componentDidUpdate` method.
Side effects are allowed during the commit phase so they can be present in the method as well, if a side effect involves a state change that change must be wrap in a condition because otherwise an infinite loop will happen.

<br>

## Fibers - React Reconciler's unit of work

A React Fiber can be described as a Rect unit of work, which React processes resulting in “finished work” which is then committed resulting in changes in the DOM.
When processing fibers React can decide to handle the work straight away or schedule it for later. <br>
The powerful aspect of this is that React can use time slicing to split the work in multiple chunks that then can be independently handling their scheduling depending on their priority. <br>
High priority work like animations can be scheduled in such a way that they are handled as soon as possible while something like a network request can be delayed a bit. <br>
Most Fibers are created during the initial mount of the React application.

<b>What is a unit of work in the context of fibers ?</b>

A change in the state of a component, a lifecycle function call or changes in the DOM are examples fo what a "unit of work" can be in the context of fibers.

Fibers have a 1:1 relationship with the different react entities which can be a DOM element or a component instance for example. <br>
<ins>The same way React generates a react element tree also the reconciler Fibers generate a tree of connected fibers like a linked list</ins>.

The type of the entity with which the fiber is related to is stored in the tag property of the fiber itself and is an integer between 0 and 24. <br>
For example, 0 is `FunctionalComponent` and 1 is `ClassComponent`, then we might have `ContextConsumer/Producer` or even `ReactFragment`.

<ins>Fiber can be created because of components but while components are recreated every time fibers are reused as much as possible to increase performances</ins>.

<b>How Fibers are reused by React?</b>

Fibers have a property called `alternate` which is basically a reference to the same fiber but on the opposite fiber tree ( current tree vs work in progress tree ).
Fibers also have a key property like a component instance, which helps identify them.
Because fibers are reused as much as possible, if React identifies that a Fiber doesn't need to be changed it will just be reused using the reference in the `alternate` property.

<br>

### Fiber structure

```TS
{
  alternate: ..., // Contains the reference to the same fiber in the opposite fiber tree
  stateNode: ..., // Contains the reference to fiber's entity
  child: ..., // Contains the reference to the first child fiber
  sibling: ..., // Contains the reference to the first next fiber sibling
  return: ..., // Contains the reference to the parent fiber,
  ...
}
```

Using all the different references contained in a Fiber React is able to traverse the tree and process the fibers in one go without recursion.

<br>

## The Fibers tree

As said before fibers form a tree but there are actually 2 fiber trees present in a React application:

- The <b>current fibers tree</b> which is basically the current representation of what is on screen.
- The <b>work in progress fibers tree</b>, which is hidden/kept in memory for performance reason, is the tree that actually receives the changes computed by React.

Once the work is done in the work in progress tree React swaps the two trees, the current tree becomes the work in progress one and vice versa in a double buffer approach.

<br>

## Effects in React

While React does most of the work asynchronously during the render phase some work like updating the DOM or lifecycle methods of components must be done synchronously during the commit phase.

For this reason, the result of the render phase is not only a tree of fibers but also a list of effects ( side effects ).

<br>

### What is an Effect?

An effect is React can be, for example, a mutation to the DOM or calling a lifecycle method and they cannot be executed during the render phase of the reconciler.

An host component event can be updating the DOM while a class component event can be calling, for example, the `componentDidMount` lifecycle method.

<br>

### When Effects are applied?

During the commit phase of the reconciler the effects are applied to all their component instances and this results in changes visible to the users.

<br>

## What are React Hooks?

React hooks were introduced in React 16.8 and they provide a way to manage state, component lifecycle and even custom logic without the need to write class components.
Basically a piece of reusable code that can be used within a component.

The following are some of the most commonly used hooks provided by React

<br>

### useState

It is hook used to access the state of a component.

```TS
const [stateValue, setStateValue] = useState(1);
```

`useState()` returns an array where the first element is the current state value and a function which is the `setter` for the `stateValue`.
As shown above, it is possible to pass the initial state value, otherwise `undefined` will be used.

The setter `setStateValue` can accept either the new state value we want to assign or it can accept a function which will receive the previous state value as a parameter. <br>

```TS
setStateValue(2);

setStateValue((previousValue) => previousValue + 1);
```

It is important to note that the setter method does not update the state straight away but rather schedule an update of the state which will be visible at the next render of the component. <br>

Passing an updater function to the `setter` provided by the `useState` hook is generally preferred because it is possible to access the previous state value which is always up to date. <br>
This is particularly useful if we need to chain multiple state updates in a single block.

For example, if we need to chain multiple state updates and we pass directly the new state value to the setter function we won't be able to see the correct result when the component re-renders because all the setter function call will use the same state value behind the scene.

```TSX
export const MyComponent: FC<MyComponentProps> = () => {
  const [value, setValue] = useState(0);
  const [otherValue, setOtherValue] = useState(0);

  useEffect(() => {
    // PASSING A NEW STATE VALUE DIRECTLY TO THE STATE SETTER
    setValue(value + 1);
    setValue(value + 1);
    setValue(value + 1);
    setValue(value + 1);

    // WHAT WE EXPECT TO HAPPEN
    // Comment this block if you plan to try out this component and remove React.StrictMode
    setValue(0 + 1);
    setValue(1 + 1);
    setValue(2 + 1);
    setValue(3 + 1);

    // WHAT ACTUALLY HAPPENS
    // Because the setter function just schedules an update
    // it uses the state value that the component currently hold
    // which in this case is 0.
    // Comment this block if you plan to try out this component and remove React.StrictMode
    setValue(0 + 1);
    setValue(0 + 1);
    setValue(0 + 1);
    setValue(0 + 1);

    // -----------------------------------------------

    // PASSING AN UPDATER FUNCTION TO THE STATE SETTER
    setOtherValue((prev) => prev + 1);
    setOtherValue((prev) => prev + 1);
    setOtherValue((prev) => prev + 1);
    setOtherValue((prev) => prev + 1);

    // WHAT WE EXPECT TO HAPPEN
    // Comment this block if you plan to try out this component and remove React.StrictMode
    setOtherValue((prev) => 0 + 1);
    setOtherValue((prev) => 1 + 1);
    setOtherValue((prev) => 2 + 1);
    setOtherValue((prev) => 3 + 1);

    // WHAT ACTUALLY HAPPENS
    // The previous value passed to the updater function will always be up to date.
    // Comment this block if you plan to try out this component and remove React.StrictMode
    setOtherValue((prev) => 0 + 1);
    setOtherValue((prev) => 1 + 1);
    setOtherValue((prev) => 2 + 1);
    setOtherValue((prev) => 3 + 1);
  }, []);

  return (
    <div>
      <h1>PASSING A NEW STATE VALUE DIRECTLY TO THE STATE SETTER: {value}</h1>
      <h1>PASSING AN UPDATER FUNCTION TO THE STATE SETTER: {otherValue}</h1>
    </div>
  )
}
```

<br>

#### Updating Objects in state

When dealing with Object in state we need to be careful when updating them, more specifically when we need to update just one of their properties.

```TS
const [state, setState] = useState<MyStateType>({ ... });
```

If when updating the `state` we just pass an object with only the updated property in the setter function we will replace the whole object in state and we will not update just the single property.

```TS
// SETUP
const myInitialState: MyStateType = {
  myFirstProperty: 1,
  mySecondProperty: 2,
  myThirdProperty: 3
};
const [state, setState] = useState(myInitialState);
```

❌ The wrong way

```TS
setState({ myThirdProperty: 0 });

// New state value result
{
  myThirdProperty: 0
}
```

✅ The Correct way

```TS
setState((prev) => { ...prev, myThirdProperty: 0 });

// New state value result
{
  myFirstProperty: 1,
  mySecondProperty: 2,
  myThirdProperty: 0
}
```

<br>

### useEffect

It is a hook used to access the component lifecycle and its effect runs after every completed render of the react application. <br>

The `useEffect` hook accepts a function as the <ins>first parameter</ins> which contains the logic to run when the useEffect hook is called. <br>
The function passed as the first parameter can also return a function that will be used as a `clean-up function` which will be called before the component is unmounted/before the next useEffect call. <br>
The <ins>second parameter</ins> that is possible to pass to the useEffect hook is an array of dependencies which will be checked to decide if the effects needs to be run or not.

<br>

#### When to avoid using the useEffect hook?

We should avoid using useEffect for event based effects as, for example, the logic associated with a specific button click. <br>
This will avoid unnecessary re-renders of the component or nasty side effects.

Avoid also to chain multiple useEffect when the things inside those use effects are dependent between each other causing a cascade of useEffect triggers.

<br>

#### When we want to use the useEffect hook?

Syncing third-party widgets that are part of an external library.
When doing subscriptions/adding event handlers.
Data fetching.
...

<br>

#### How to use the useEffect hook

Depending on what is specified within the `dependencies array` as second parameter the `useEffect` hook will behave differently.

<br>

##### useEffect hook dependant on every state/prop change

```TS
useEffect(() => {
  console.log('Component rendered');

  return () => console.log('Component will be unmounted');
});
```

Setting up the `useEffect` hook without specifying an array of dependencies will make the effect logic contained in the function passed to the hook run at every state or prop change alongside the first render of the component.

<br>

##### useEffect hook dependant on specific state changes/prop changes

```TS
useEffect(() => {
  console.log('Component rendered');

  return () => console.log('Component will be unmounted');
}, [stateValue, testProp]);
```

Setting up the `useEffect` and specifying an array of dependencies with some entries will make the effect logic run only when there are changes to the dependencies passed to the `useEffect` hook.

<br>

##### useEffect hook defined with an empty dependencies array

```TS
useEffect(() => {
  console.log('Component rendered');

  return () => console.log('Component will be unmounted');
}, []);
```

Because the dependencies array is empty then the effect is not dependent on state or props changes, meaning that the effect will run once when the component is actually rendered the first time and once before the component is unmounted if a clean-up function is returned. <br>
This approach is particularly useful when we need to apply some logic (i.e. fetching data) only when the component is rendered.

<br>

### useLayoutEffect

The `useLayoutEffect` hook is similar to useEffect and the main difference is when the effect of the hook is actually triggered.

While the `useEffect` hook runs after the whole component has been rendered the `useLayoutEffect` hook runs <b>before</b> the component has rendered but <b>after</b> the JSX tree has been adjusted with the latest updates.

This makes the useLayoutEffect hook very handy when it is necessary to update some styling dynamically, adjust scroll values or modify the DOM while avoiding flickering for example.

Similarly to the useEffect hook also the function passed as parameter of the useLayoutEffect hook can return a function which will then be used before the component is unmounted.

Also, as the `useEffect` hook, the `useLayoutEffect` hook accepts an array of dependencies as the second parameter to control when it should be fired and its behavior is exactly the same as `useEffect`. <br>
So, if no array of dependencies is passed to the useLayoutEffect hook the layout effect will be triggered at every re-render of the component. <br>
If an array of dependencies is passed to the hook but it is empty, the layout effect will be triggered only during the first render of the component while if dependencies are specified it will be triggered only when those dependencies will change.

<br>

### useRef

The `useRef` hook is used to store mutable state that doesn’t change when the component is re-rendered and also a change to a ref doesn’t trigger the re-render of the component. <br>
Most of the time it is used to access and manipulate DOM elements but it is also possible to store mutable values that persist across re-renders without triggering a re-render when the mutable value changes. <br>
Also it is used for storing instance variables.

<br>

#### Ref Forwarding

It is possible to create a Ref and then pass it down from a parent to a child component.
This is particularly useful if, for example, we need to access a specific DOM element of a child component from the parent or if we want to create a custom hook that needs access to a DOM node.

Because the `ref` property is not accessible from the `props` property inside a component we need to explicitly tell react that we want to forward a ref during the component declaration.

```TSX
// Defining a Child component which will accept a ref forwarded by its parent
interface MyChildProps {
  value: string
}

const MyChild = React.forwardRef<HTMLDivElement, MyChildProps>((props, forwardedRef) => {
  return (
    <div ref={ref}>
        My Child Component
    </div>
  );
});

// Defining the Parent component
export const MyParent = () => {
  const childComponentDivRef = useRef<HTMLDivElement>(null);

  // In this way the parent will have access to the DOM node (div) of the child
  return (
    <div>
      <MyChild ref={childComponentDivRef} />
    </div>
  );
}
```

Another use case to use the hook useRef is when dealing with forms. <br>
If we use useState to handle the state of every single field in the form every time the user input a value in one of the available fields the component will re-render which is not exactly ideal. <br>
To avoid situations like this it is possible to define refs for fields in the form and access their value only when, for example, the form is submitted. <br>
Because the value itself of each single field is not tied up with the component state the component itself won’t re-render.

<br>

### useImperativeHandler

The `useImperativeHandler` hook allows us to specify and expose custom properties or methods of a forwarded ref. <br>
It is particularly useful when defining complex behavior of general components such as, for example, an input component where we need to be able to call a method directly using its ref from the parent or access a custom property of the ref from the parent.

```TSX
// Defining our Child component
interface MyChildRefInstance {
  changeBackgroundColor: () => void;
}

export const MyChild = React.forwardRef<MyChildRefInstance, MyChildProps>((props, forwardedRef) => {
  const localRef = useRef<HTMLDivElement>(null);

  useImperativeHandle(forwardedRef, () => {
    changeBackgroundColor: () => {
      if (localRef.current) {
        localRef.current.style.backgroundColor = "green";

        setTimeout(() => {
          localRef.current.style.backgroundColor = "red";
        }, 1000);
      }
    }
  });

  return (
    <div ref={localRef}>
      My Child component
    </div>
  );
});
```

Within the `MyChildComponentInstance` interface we define the custom properties/methods we want to add to our ref.

We use the `useImperativeHandle` by passing the forwardedRef to it to tell React that the ref will be receiving some custom logic. <br>
The second argument of the hook is a function that returns an object in which we can define our custom properties/methods logic.

```TSX
export const MyParent: FC = () => {
  const childComponentRef = useRef<MyChildRefInstance | null>(null);

  useEffect(() => {
    if (childComponentRef.current) {
      childComponentRef.current.changeBackgroundColor();
    }
  });

  return (
    <div>
      <MyChild ref={childComponentRef} />
    </div>
  );
};
```

<br>

### useContext

The `useContext` hook gives us access to the React Context API. <br>
Context in React is something that can be passed down to all components wrapped around a `<React.ContextProvider>` without the need to pass it through props. <br>
Context can be anything, a complex object representing a state, a number, string or event methods … <br>
The useContext can be used by components to access the value of the context.

It is also possible to pass a `default value` to our Context that will actually only be used when a component is trying to access the context but the component itself is not wrapped by its matching `Context Provider`.

If we want a global context we can simply wrap the whole app with a `Context Provider` and all components within the app will be able to access its value. <br>
This is useful in situations such, for example, theming or situations where multiple components that might not have a Parent-Child relationship might need to access the same state like the authentication status of the user for example.

```TSX
// Defining the context
export const MyContext = createContext("Context default value");

// Setting up a Context Provider for my Child Component
export const MyParentComponent: FC = () => {
  return (
    <MyContext.Provider value="My initial context value">
      <MyChildComponent />
    </MyContext.Provider>
  );
}

// Defining the Child Component
const MyChildComponent: FC = () => {
  const contextValue = useContext(MyContext);

  return (
    <div>
      Context Value: {contextValue}
    </div>
  );
}
```

<br>

### useReducer

With the `useReducer` hook we can increase the control we have on our application state making everything more organized and predictable in situations when we need to handle very complex states. <br>
<ins>When we want to update our state instead of using a setter function we dispatch an action.<ins>

The `userReducer` hook requires 2 parameters:

- A reducer
- A state initial value

The reducer required by the `useReducer` hook is a function which accepts the current state and the dispatched action as arguments. <br>
Everything is more organized because instead of just passing a new value for our state we can actually execute different bits of logic depending on the action dispatched.

```TSX
enum ReducerAction {
  Increment: 'increment',
  Decrement: 'decrement'
}

type MyStateType = {
  counter: number
}

type ActionType = {
  type: string
}

const myInitialStateValue: MyStateType = { value: 5 };

const myReducer = (myState: MyStateType, action: ActionType): MyStateType => {
  switch(action.type) {
    case ReducerAction.Increment:
      return {
        ...myState,
        counter: myState.counter + 1
      };
    case ReducerAction.Decrement:
      return {
        ...myState,
        counter: myState.counter -1
      };
    default:
      return myState;
  }
}

export const MyComponent: FC = () => {
  const [myState, dispatcher] = useReducer(myReducer, myInitialStateValue);

  return (
    <div>
      <button onClick={() => dispatcher({ type: ReducerAction.Increment })}>+</button>
      <button onClick={() => dispatcher({ type: ReducerAction.Decrement })}>-</button>
    </div>
  );
}
```

<br>

### useMemo

The `useMemo` hook memoizes the value returned by the method passed as parameter and re-compute it only when the passed dependencies actually change, avoiding unnecessary computations. <br>
This hook is very useful to improve the performance of a component that needs to perform intensive computations which result might be only influenced by a change in the component props/or doesn't change very ofter.

```TS
const filteredPosts = useMemo(() => {
  return myListProp.filter((post: Post) => post.body.includes(myWordProp));
}, [myWordProp]);
```

In this case the return value of the hook will be re-computed only when the `myWordProp` changes.

If we don’t pass any dependency to the dependency array in the second argument of the `useMemo` hook the memoized value will be computed at the first render of the component and will be stored until its unmounted without changes. <br>

<br>

### useCallback

While `useMemo` memoizes a value the `useCallback` hook memoizes a callback function. <br>
This is particularly useful when passing handler methods to a child component while avoiding triggering their re-render every time the function is passed to the child component as prop. <br>
This happens because when the parent component re-renders the function defined in its body are recreated every time meaning that in memory they will be placed in a different address making them look like they are a totally new function/prop by the child component.

```TS
const onDeleteHandler = useCallback(() => {
  doSomethingWithAStateValue(stateValue);
}, [stateValue]);
```

In this case if we pass this function to a child component and then the stateValue changes in the parent component then and only then the child component will be re-rendered because one of its props have changed (assuming it is its only prop and there aren’t other things going on within the component).

<br>

### useDeferredValue

The `useDeferredValue` hook can be used in scenarios where we have a slow component that is being rendered causing delay in inputs or general responsiveness degradation. <br>
If, for example, we have a value that is passed down to a child component as a prop and that value is updated through an input field present in the parent component, every time that value changes we are going to experience a re-render of the child component which cause the parent to become slightly unresponsive due to the child component slowness. <br>
By passing the value to the child component wrapped around a useDeferredValue hook it is possible to defer the update of that specific value reducing the number of re-renders of the child component. <br>
The child component must be provided using the HOC `React.memo` to gain the full benefits of this feature.

<br>

## Custom Hooks

In React it is possible to define custom hooks with custom logic to accommodate the needs of our application.

```TS
const useLocalStorageCustomHook = (localStorageKey: string, defaultValue?: string) => {
  const [value, setValue] = useState(() => {
    const currentLocalStorageValue: string = localStorage.getItem(localStorageKey);
    return currentLocalStorageValue
      ? JSON.parse(currentLocalStorageValue)
      : defaultValue;
  });

  const setNewValue = (newValue: string | Function) => {
    const valueToSet = (newValue instanceof Function)
      // We pass the current value of the hook so if an updater function is passed to the
      // setter of this custom hook it will have access to the current, most up to date,
      // state value as it happens with useState
      ? newValue(value)
      : newValue;

      localStorage.setItem(localStorageKey, JSON.stringify(valueToSet));
      setValue(valueToSet);
  }

  return [value, setNewValue];
}
```

<br>

## Why Hooks cannot be used inside a loop or a condition block ?

React hooks rely on call order because everything with hook revolves around `arrays and indexes` to manage the state and so it is not possible to call hooks inside loops or in a condition block because the next time a component re-renders it might happens that a condition block might not be executed or the number of iterations of a loop might be different than before messing up the indexes and finally the state.

<br>

## Why using a State Management Library in React ?

While a `context + reducer` combination might be a good idea to handle rather complex single component state, when it comes to efficiently handling the state of a whole application/group of components that might become tricky.

In the scenario stated above it is better to prefer state management libraries instead of building something “in house” for the following reasons:

- <b>Performances</b>

  State management libraries are optimized to be performant

- <b>Middleware support</b>

  Some state management libraries, such as `Redux`, offer the ability to define `middlewares` that are triggered on specific dispatch events providing the ability to add custom functionalities to it and easily add things like, logging, error management, ect. ect.

- <b>Scalability</b>

  Because state management libraries provide you a structured way of defining your state it is easier to scale a React application and the overall code will be more maintainable.

- <b>Persisting state across re-renders across multiple components/pages</b>

  Let’s say that we have a stepper component which includes some forms and other bits that a user needs to fill in. <br>
  If the user goes back to another view/page of the react application and then back again to our stepper component with the help of a state management library we could store the state of the stepper component when the user is actually interacting with it and resume it with the same exact state if needed.

<br>

## React.memo & Pure Components

`React.memo` is `HOC ( High-order components )` that accepts a component as first parameter and return an enhanced version of it that allows us to take control over when our component should be re-rendered, more specifically with React.memo a component only rerenders when its props changes stopping it from rerendering, for example, when its parent component re-renders (if no custom props comparison logic is passed to the React.memo function).

This type of components are well suited when we have components that change only when their props change, simple components in general or components that render static content.

The checks on the props is a shallow comparison so for complex props checking it is better to pass to `React.memo` a comparison function alongside the component.<br>
The comparison function passed as second parameter will have access through its parameters to the previous set of props and the new set of props with which it is possible to do complex equality checking/custom logic to determine if the component should actually re-render or not. <br>
This is especially useful if the child component has some heavy logic running during its render which can slow down performances.

Because <ins>it is not possible to use React.memo with class components</ins> to achieve the same result instead of extending the component class with the Component class we need to extend the component class with the PureComponent class and add additional logic ( if needed ) in the `shouldComponentUpdate` method. <br>
A caveat of class components and the `shouldComponentUpdate` method is that a class component will re-render even if the previous state is exactly the same as the old one so it is necessary to add checks for that as well alongside checks for the props.

<br>

## HOC (High-order component)

High-order components are used in React to add functionalities, props, custom logic to components without duplicating code.
They follow the same logic of high-order function and so a high-order component is a function that returns a component with enhanced capabilities.

```TSX
const MyComponent: FC<MyComponentProps> = () => {
  return (
    <div>
      <h1>My Component</h1>
    </div>
  );
}

const withAuthHOC = (WrappedComponent: FC) => {
  return (props: any) => {
    const navigate = useNavigate();
    const isUserAuthenticated = getUserAuthStatus();

    if (!isUserAuthenticated) {
      navigate('/login');
    }

    return <WrappedComponent {...props} />
  }
}
```

<br>

## Error Boundaries in React

If a component experiences an error during its rendering phase the whole React application will turn in a white page making a horrible user experience. <br>
For this reason, it is necessary to set some error boundaries to avoid the scenario above from happening and to have better control over the state of the application.

<ins>To create an error boundary we must use a class component because of the need to access and use the static lifecycle method `getDerivedStateFromError` which is present only for class components.</ins> <br>
We use the static method `getDerivedStateFromError` to actually be able to catch the error before the actual rendering of the component happens.

When a component throws an error during rendering React will start traverse the component tree upwards to try find an Error Boundary and if it finds it then it proceeds in executing its side logic.
If, for some reason, also the error boundary found by throws an error, React will continue traversing the component tree upwards trying to find another one that will catch the error. <br>
This behavior of React allows us to set `local & global error boundaries` depending on the scenario we are facing and application specific needs.

It is important to state that errors thrown, for example, by some asynchronous code that finish running after the component is actually rendered will NOT be caught by the Error boundary but we would need to set up on our own some logic to display a different state of our component when that error is thrown.

```TSX
type MyErrorBoundaryState = {
  hasError: boolean
}

interface MyErrorBoundaryProps {
  fallback: ReactNode,
  children: ReactNode
}

export class MyErrorBoundary extends Component<MyErrorBoundaryProps> {
  state: Readonly<MyErrorBoundaryState> = {
    hasError: false
  }

  static getDerivedStateFromError(): MyErrorBoundaryState {
    return { hasError: true };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo): void {
    console.log(error, errorInfo);
    loggingService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback;
    }

    return this.props.children;
  }
}

const ErrorStateComponent: FC = () => {
  return <h1>An error happened</h1>;
}

const MyChildComponentWithError: FC = () => {
  const throwError = () => {
    throw new Error('Test error');
  }

  return <button onClick={() => throwError()}>Throw an error</button>
}

export const MyComponent: FC = () => {
  return (
    <MyErrorBoundary fallback={<ErrorStateComponent />}>
      <MyChildComponentWithError />
    </MyErrorBoundary>
  );
}
```

<br>

## Suspense in React

Suspense is a React component that allows us to wait for some asynchronous operations happening in/for the components wrapped by it before actually rendering them while displaying a fallback/loading component/state during the waiting time. <br>
<ins>It works like async/await but for components</ins>.

This is particularly useful for `lazy loading components` or `data fetching` using those third-party libraries that support Suspense (i.e. React query).

```TSX


const LoadingState: FC = () => {
  return <h1>Loading...</h1>;
}

const ErrorState: FC = () => {
  return <h1>Error</h1>;
}

const MyChildComponent: FC = () => {
  const { data, isPending, error } = useQuery({
    queryKey,
    queryFn,
    suspense: true // Necessary to activate the "suspense mode" in React Query
  });

  // Because we use Suspense we don't need this kind of condition block to
  // display a loading state.
  // Everything regarding loading will be handled by React Query & Suspense Component
  // if (isPending) {
  //   return <LoadingState />;
  // }

  if (error) {
    return <ErrorState />;
  }

  return (
    <div>
      <pre>
        {JSON.stringify(data, null, 2)}
      </pre>
    </div>
  );
}

export const MyComponent: FC = () => {
  return (
    <Suspense fallback={<LoadingState />}>
      <h1>My Data</h1>
      <MyChildComponent />
    </Suspense>
  );
}
```

In this example if the `MyChildComponent` was using ReactQuery with the suspense parameter set to true, the component will be rendered only when the async data fetching logic has resolved returning the data for the component. <br>
Also the `h1` element wrapped within the same Suspense block will be rendered only when the `MyChildComponent` finishes its async task because Suspense waits for all of the components wrapped by it to be available before actually rendering them. <br>
It is an <ins>all or nothing</ins> kinda of rendering logic.

```TSX
export const MyComponent: FC = () => {
  return (
    <Suspense fallback={<LoadingState />}>
      <h1>My Data</h1>
      <MyChildComponent />
      <Suspense>
        <OtherComponent />
      </Suspense>
    </Suspense>
  );
}
```

In the example above we know that `MyChildComponent` will always take less to import & render than the `OuterComponent` so we wrap the slower component in its own nested `Suspense` block and the other components in the block above. <br>
In this example the two different sets of components can render whenever they are available without waiting for one another.

Because `Suspense` waits for all its children before actually rendering them all, if we have components with async operations going on or we are lazy loading components that might require different time to be downloaded, mounted and rendered, it is possible to use nested Suspense blocks to avoid waiting for all components. <br>
It this way each `Suspense bloc` will be rerendered at different times.

<br>

### Error handling in Suspense

To properly handle errors that can happen during the suspended phase we need to use an ErrorBoundary.

```TSX
export const MyComponent: FC = () => {
  return (
    <MyErrorBoundary fallback={<ErrorState />}>
      <Suspense fallback={<LoadingState />}>
        <h1>My Data</h1>
        <MyChildComponent />
        <Suspense>
          <OtherComponent />
        </Suspense>
      </Suspense>
    </MyErrorBoundary>
  );
}
```

<br>

## React.lazy

`React.lazy` is an alternative way to import components that allows us to decide when their actual code is being downloaded & rendered. <br>
This is a great deal when it comes to performance because we can decide when the code of some child components is actually downloaded, avoiding downloading code that, for example, is not going to be rendered due to specific conditions. <br>

<ins>React.lazy requires the use of Suspense to work</ins>.

Depending if you are using default export or named export you will need to use `React.lazy` in a different way because it expects an object with a property `default` that contains the actual component code which is not present for named exports. <br>

```TS
// Default export
const DefaultExportComponent = React.lazy(() => import('./DefaultExportComponent'));

// Named export
const NamedExportComponent = React.lazy(() =>
  import('./NamedExportComponent').then(module => ({ default: module.NamedExportComponent}))
)
// With named exports we basically need to shape the imported code in the way that React.lazy expects it.
```

<br>

## What are Portals in React?

Portals in React provide a way to take some content inside React and render it somewhere else. <br>
Because portals interact with the DOM it comes from the renderer and not React itself.

To use portals we can import the createPortal method from the renderer library (ReactDOM for example) and pass to it the JSX that needs to be rendered plus the location where we want to render it (an HTML node).

```TSX
export const MyComponent: FC = () => {
  return createPortal(
    <Suspense fallback={<LoadingState />}>
      <h1>My Data</h1>
      <MyChildComponent />
    </Suspense>
  , document.body);
}
```

<br>

## Controlled Vs. Uncontrolled Components

### Uncontrolled Components

Uncontrolled components are components that have ownership of their own state and release that state only when a specific event happens, such as, a form submit button click. <br>
Before the event fires it is not possible to access the full state of the uncontrolled component. <br>
For example an uncontrolled component involving a form would see the input fields being handled through refs and only on a submit submit click the value from the refs is extracted

### Controlled Components

Controlled components are components which are controlled by their parent including their state which is passed down to them as a prop alongside event handlers and other bits or components that have a bi-directional control over the state where the state is accessible at any give point in time<br>
For example a controlled `form` component would use `useState` to define the form state properties and use those to control the state of the different inputs in the form. <br>
Controlled components involving forms give the ability to do input validation while the user is typing instead of waiting for the submit of the form thanks to the two way binding that the use of `useState` brings with its use.

Another example of a controlled component is a `Modal` where we would usually pass to it a prop to define if the modal should be shown alongside a method to be called when the modal is closed.

Last example, in case we have a `Stepper component`, set up as a controlled component, it will be possible to conditionally decide which steps to show or not to show with a controlled component implementation because we have direct access to the state of the stepper component and from the parent we can directly react to changes to the state and decide if a specific step should be shown or not ( in cases where, for example, depending on specific conditions we might have more steps to show or less ).

<br>

## Controlled Vs. Uncontrolled Inputs

Similarly to controlled/uncontrolled components we have a controlled input when the value and the on change behavior of the input is controlled by the component itself by using, for example, `useState` to track the value and a `onChange` handler function.

```TSX
// Controlled Input
export const MyControlledInputComponent: FC = () => {
  // Because of the use of useState to keep track of the state of the field we
  // can access the field
  const [value, setValue] = useState('');

  return (
    <form>
        <label htmlFor="nameField">Name</label>
        <input
          name="name"
          id="nameField"
          value={value}
          onChange={(e) => setValue(e.currentTarget.value)} />
    </form>
  );
}

// Uncontrolled Input
export const MyUncontrolledInputComponent: FC = () => {
  const onSubmit = (e) => {
    e.preventDefault();

    // We are able to access the state of our form only during submission
    const nameValue = e.currentTarget?.elements.name.value;
  };

  return (
    <form onSubmit={onSubmit}>
        <label htmlFor="nameField">Name</label>
        <input
          name="name"
          id="nameField" />
    </form>
  );
}
```

<br>

## Where should I store the state of my component?

If the state of the component is used only within the component itself then the state of the component should be as local as possible and so within itself.

If the state of a particular component could potentially influence the behavior of other components then the best place to store the state is within the closest Parent component for both children.

<br>

## Compound Component

Often there are components which include several different sections which can become really messy really fast when it comes to passing the right content to them through props making them difficult to understand. <br>
Compound components are components that offer a better organization of its content and provide a better control over their different sections and an overall better way to compose your component which results in simpler code and a DX.

```TSX
// NOT A COMPOUND COMPONENTS
interface MyCardProps {
  children?: ReactNode,
  header: ReactNode,
  footer: ReactNode
}

export const MyCard: FC<MyCardProps> = ({ children, header, footer }) => {
  return <div>
    {header && <div
      style={{
          borderBottom: '1px solid black',
          fontSize: '20px',
          padding: '3px',
      }}>{header}</div>
    }
    <div
      style={{
          backgroundColor: 'red',
          fontSize: '20px',
          marginTop: '20px',
          padding: '3px',
      }}>{children}</div>
    {footer && <div
      style={{
          borderTop: '1px solid dashed',
          fontSize: '20px',
          padding: '3px'
      }}>{footer}</div>
    }
  </div>
}

export const ParentComponent: FC = () => {
  return <div>
    <h1>This is my card page</h1>
    <p>Some additional text</p>
    <MyCard
      header={<h1>This is the header of my card component</h1>}
      footer={<div>
        <h3>This is the footer of my card component</h3>
        <h5>Some links</h5>
        <ul>
          <li>Link 1</li>
          <li>Link 2</li>
          <li>Link 3</li>
        </ul>
      </div>}
    >
      <p>This is the body of my card component</p>
    </MyCard>
  </div>
}
```

```TSX
// A COMPOUND COMPONENT
import React from "react";

interface MyProps {
  children?: React.ReactNode;
}

export const MyCard = ({ children }: MyProps) => {
  return <div>{children}</div>;
};

const Header: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  return (
    <div
      style={{
        borderBottom: "1px solid black",
        fontSize: "20px",
        padding: "3px",
      }}
    >
      {children}
    </div>
  );
};

const Body: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  return (
    <div
      style={{
        backgroundColor: "red",
        fontSize: "20px",
        marginTop: "20px",
        padding: "3px",
      }}
    >
      {children}
    </div>
  );
};

const Footer: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  return (
    <div
      style={{
        borderTop: "1px solid dashed",
        fontSize: "20px",
        padding: "3px",
      }}
    >
      {children}
    </div>
  );
};

MyCard.Header = Header;
MyCard.Body = Body;
MyCard.Footer = Footer;

export const ParentComponent: React.FC = () => {
  return (
    <div>
      <MyCard>
        <MyCard.Header>
          <h1>This is the header of my card component</h1>
        </MyCard.Header>
        <MyCard.Body>
          <p>This is the body of my card component</p>
        </MyCard.Body>
        <MyCard.Footer>
          <div>
            <h3>This is the footer of my card component</h3>
            <h5>Some links</h5>
            <p>Some other text</p>
          </div>
        </MyCard.Footer>
      </MyCard>
    </div>
  );
};

```

<br>

## Cloning a Component

If we need to update the props of a child component that is passed to the Parent within the children props React provides a way for us to clone that component and update the props that were passed to it.

```TSX
// The React.Children.toArray helps us in case we have only 1 children passed down
const firstChildren = React.Children.toArray(children)[0];

// Then we check that the child component picked is a valid element
if (React.isValidElement(firstChildren)) {
  return React.cloneElement(firstChildren, { ...myUpdateProps });
}
```

<br>

## React project folder structure

For medium to large project ( opinionated example ).

- assets
- components - Global/Shared components folder
  - ui - ui components only i.e. Button, TextField, ...
  - form: form components
  - ...
- context - folder where all global context are defined
- data - global static data
- hooks - custom hooks folder
- pages
- utils
- feature - collection of components that together create a feature i.e. auth, settings, ...
  - the inner feature folder structure should mimic the root folder structure
- types

<br>

# React router

Routing can be hard and it is better to use some kind of libraries such as React Router to handle it.

It is possible to do some basic routing adding some custom logic to our host component to display specific components depending on the route using `window.location.pathname` & `links (a tags)` but this approach is not robust enough for even medium application and brings with itself some performance issues as, for example, full browser page refresh every time we change a route and consequent re-download of all html, js and assets every time. <br>
Also, dealing with nested routes and/or dynamic routing becomes almost impossible to do efficiently.

<br>

## Simple React router implementation

```TSX
// router.tsx
import { createBrowserRouter } from "react-router-dom";
import { Home, About, Profile, RouteNotFound } from './Pages';

export const router = createBrowserRouter([
  { path: '/', element: <Home /> },
  { path: '/about', element: <About /> },
  { path: '/profile', element: <Profile /> },
  // Fallback route to display a 404 page
  { path: '*', element: <RouteNotFound />}
  // Alternatively it is possible to redirect the user directly using the <Navigate /> component
  { path: '*', element: <Navigate to="/" /> }
]);

// App.tsx
import { StrictMode } from "react";
import { RouterProvider } from "react-router-dom";
import { router } from './router';

export const App = () => {
  return (
    <StrictMode>
      <RouterProvider router={router} />
    </StrictMode>
  );
}
```

One thing to mention is that React router always renders matching routes starting from the top of the defined routes in the router. <br>
Also, routes that are more specific have the priority, so for example, a dynamic route will have a lower priority than a perfect match even when the dynamic route is placed before the route with a perfect match. <br>
So it will check one by one the array content and children content ( if present ) until it finds a matching route. <br>
That’s why it is recommended to always add a fallback route at the end of the array with a 404 page.

<br>

## Navigation

When using React router to navigate between pages in your React application it is necessary to use the `Link` or `NavLink` component provided by React router so it will be possible to avoid using standard html link which would trigger a full page refresh in the browser when used and so avoiding to re-download all html, assets and js from the server at every page change.

```TSX
// SIMPLE COMPONENT

export const MyComponent: FC = () => {
  return (
    <div>
        <h1>My Component</h1>
        <Link to="/">Go to Home Page</Link>
    </div>
  );
}

// NAV COMPONENT

// NavLink is to be used in a Nav component because of its behavior when a specific route is selected.
// React router automatically adds an .active class to the NavLink component so it will
// be possible to easily apply a specific style to those links when their linked page is selected.

export const Nav = () => {
  return (
    <nav>
      <ul>
        <li>
          <NavLink to="/">Home</NavLink>
        </li>
        <li>
          <NavLink to="/about">About</NavLink>
        </li>
        <li>
          <NavLink to="/profile">Profile</NavLink>
        </li>
      </ul>
    </nav>
  );
}
```

It is also possible to define relative paths in the Link component.
For example, it is possible to pass “..” to make React Router go back one level in the tree.

<br>

## Nested Routes

By using nested routes with React Router it is possible to define sub routes for a specific route with the ability to provide, for example, a common container or Layout for the sub-routes specified.

```TSX
// router.tsx
export const router = createBrowserRouter([
  { path: '/', element: <Home /> },
  { path: '/about', element: <About /> },
  { path: '/profile', element: <Profile /> },
  {
    path: '/team',
    element: <TeamPageLayout />, // Common layout that will host the components of the child routes
    children: [
      // Setting index: true will guarantee that the component defined in the route is rendered
      // only when a full/perfect match of the route exists, so in this case "/team"
      { index: true, element: <Team /> },
      // After the first route specification for the parent route we define the sub-routes
      { path: 'performances', element: <TeamPerformances /> },
      { path: 'settings', element: <TeamSettings /> }
    ]
  }
]);

// TeamPageLayout.tsx
...
import { Outlet } from "react-router-dom";

// The Outlet component provided by React Router will be in charge of displaying the component element
// specified in the element property in the route object.
// In this way it is easy to place the content right where it should go and style pages accordingly.

export const TeamPageLayout: FC = () => {
  return (
    <div>
      <h1>This is the Team Page Layout</h1>
      <Outlet />
    </div>
  );
}
```

<br>

### Outlet Context

Another powerful feature of React Router is the ability to pass a context prop to the outlet used by the router to display the component element specified in the router object.
Then it is possible to access that context from the sub-routes defined by using the `useOutletContext` hook provided by React Router.

```TSX
export const TeamPageLayout: FC = () => {
  return (
    <div>
      <h1>This is the Team Page Layout</h1>
      <Outlet context="This is my Outlet Context value" />
    </div>
  );
}

export const TeamSettings: FC = () => {
  const outletContextValue = useOutletContext() as string;

  return (
    <div>
      <h1>Team Settings page</h1>
      <p>This is the Outlet context value: {outletContextValue}</p>
    </div>
  );
}
```

<br>

### Global Layout

```TSX
export const router = createBrowserRouter([
  {
    element: <GlobalLayout />,
    children: [
      { path: '/', element: <Home /> },
      { path: '/about', element: <About /> },
      { path: '/profile', element: <Profile /> },
      {
        path: '/team',
        element: <TeamPageLayout />,
        children: [
          { index: true, element: <Team /> },
          { path: 'performances', element: <TeamPerformances /> },
          { path: 'settings', element: <TeamSettings /> }
        ]
      }
    ]
  },
]);
```

<br>

## Dynamic Routes

React Router provides an easy way to define dynamic URI parameters for a specific route.

```TSX
export const router = createBrowserRouter([
  {
    element: <GlobalLayout />,
    errorElement: <GlobalError />,
    children: [
      { path: "/", element: <Home /> },
      { path: "/about", element: <About /> },
      { path: "/profile", element: <Profile /> },
      {
        path: "/team",
        errorElement: <TeamError />,
        element: <TeamPageLayout />,
        children: [
        { index: true, element: <Team /> },
        { path: 'performance', children: [
          { index: true, element: <TeamPerformances />, },
          { path: ':teamMemberId', element: <TeamMemberPerformance /> }
        ] },
        { path: 'settings', element: <TeamSettings /> },
      ]}
    ]
  }
]);
```

<br>

## useNavigate React Router Hook

```TSX
export const MyComponent: FC = () => {
  const navigate = useNavigate();

  return (
    <div>
      <h1>Team Settings page</h1>
      <button onClick={() => navigate('/')}>Go to Home Page</button>
    </div>
  );
}
```

<br>

## Loaders

Loaders are a powerful feature of React Router that allows us to fetch data ( or send any kind of request, i.e. some logging or analytics ) when a specific route is visited and pass it to the component.

To access the data that is computed within a loader function React router provides a `useLoaderData` hook that can be used within components.

React router also provides a `userNavigation` hook that will return the state of the router for a specific route ( idle, submitting [ for forms submission ], loading ) which comes really handy to understand when the loader is still waiting for a response from a server and display the appropriate status on page.

```TSX
// router.tsx
export const router = createBrowserRouter([
  {
    element: <GlobalLayout />,
    errorElement: <GlobalError />,
    children: [
      { path: "/", element: <MyFormComponent /> },
      { path: "/about", element: <About /> },
      {
        path: "/profile/:userId",
        element: <Profile />,
        // Executes on GET requests
        loader: ({ params, request }) => {
          // We can access the dynamic parameter in the URI
          console.log(params.userId);
          return axios.get("https://jsonplaceholder.typicode.com/posts", {
            signal: request.signal,
          });
        },
      },
    ],
  },
]);

// MyComponent.tsx
export const MyComponent: FC = () => {
  const dataFromLoader = useLoaderData();
  const { state } = useNavigation();

  if (state === 'loading') {
    return <h1>Loading...</h1>;
  }

  return (
    <div>
      <h1>My Component</h1>
      <pre>
        {JSON.stringify(loaderData, null, 2)}
      </pre>
    </div>
  );
}
```

The `loading state` is provided every time a loader function is being called and we are waiting for a response while the submitting state is provided when calling and waiting for an action (i.e. when submitting a form with an action property different than a GET ). <br>
The loader function is not strictly related to fetching data only but other logic could be executed there and the result could be passed to the component.

<br>

## Actions

When submitting forms it is possible to specify a different kind of action, HTML standard forms allow for two actions, GET and POST but React Router provides a Form component that is able to handle PATH, PUT and DELETE. <br>
Through the router it is possible to specify custom logic to be executed for actions different from GET (because by default GET requests will go through the loader function).

To access the data returned by an action we can use the `useActionData` hook provided by React Router.

```TSX
// router.tsx
export const router = createBrowserRouter([
  {
    element: <GlobalLayout />,
    errorElement: <GlobalError />,
    children: [
      { path: "/", element: <MyFormComponent /> },
      { path: "/about", element: <About /> },
      {
        path: "/profile/:userId",
        element: <Profile />,
        // Executes on GET requests
        loader: ({ params, request }) => {
          console.log(params.userId);
          return axios.get("https://jsonplaceholder.typicode.com/posts", {
            signal: request.signal,
          });
        },
        // Executes on POST, PUT, PATCH, DELETE requests
        action: async ({ request }) => {
          const formData = await request.formData();
          return axios.post(
            "https://jsonplaceholder.typicode.com/posts",
            // The formData is a Set so we need to convert it to a JSON object
            Object.fromEntries(formData.entries() || [])
          );
        },
      },
    ],
  },
]);

// MyComponent.tsx
export const MyComponent: FC = () => {
  const dataFromAction = useActionData();
  const { state } = useNavigation();

  // A state equal to "submitting" means that we are waiting for the action to return a value.
  // Note that we don't use "loading" which is reserved to loaders.
  if (state === 'submitting') {
    return <h1>Loading...</h1>;
  }

  return (
    <div>
      <h1>My Component</h1>
      <pre>
        {JSON.stringify(dataFromAction, null, 2)}
      </pre>
    </div>
  );
}
```

It is also possible to trigger actions programmatically within a component using the `useSubmit` hook.

```TSX
export const MyComponent: FC = () => {
  const [ counter, setCounter ] = useState('');
  const submit = useSubmit();

  const handleSubmission = () => {
    submit(counter, { method: 'delete', action: '/profile/123' });
  }

  return (
    <div>
      <h1>Counter Value: {counter}</h1>
      <button onClick={() => setCounter((prev) => prev + 1)}>+</button>
      <button onClick={() => setCounter((prev) => prev - 1)}>-</button>
      <button onClick={() => handleSubmission()}>Submit counter</button>
    </div>
  );
}
```

<br>

## Error handling with React Router

When defining our routes in our router object it is also possible to define an `errorElement` property for each route or group of routes that will be considered as the fallback element in case some issues happen during the rendering of the route element, basically it will behave like an `ErrorBoundary` component.

```TSX
export const router = createBrowserRouter([
  {
    element: <GlobalLayout />,
    errorElement: <GlobalErrorComponent />,
    children: [
      { path: "/", element: <MyFormComponent /> },
      { path: "/about", element: <About /> },
      {
        path: "/profile/:userId",
        element: <Profile />,
        errorElement: <LocalErrorComponent />
      },
    ],
  },
]);
```

<br>

## Async React Router

React router provides also a set of hooks, functions and components such as, `defer`, `useAsyncData`, `Await` that can be used to handle lazy loading components or async loader operations.

To use these features we need to adjust our loader in our routes to return its value wrapped with the `defer` function. <br>
This will tell React Router that we want to `hijack the loading handling` and we want to use the `Suspense` component to handle our loading logic.

```TS
export const teamPageLoader = ({ request }: { request: Request }) => {
  const req = axios.get("https://jsonplaceholder.typicode.com/posts", {
    signal: request.signal,
  });

  // The values within the object passed to the defer method as parameters
  // must be async functions
  return defer({ dataPromise: req });
};
```

After wrapping the return value of our loader with the defer function we can proceed in implementing the handling of the components using `Suspense` and `Await` alongside three other hooks `useLoaderData`, `useAsyncValue` and `useAsyncError`.

```TSX
export const MyParentComponent: FC = () => {
  // First thing we get the promise produced by the loader function and after setting up a Suspense wrapper
  // we use the Await component provided by React Router to wrap the component that will consume the data.
  const { dataPromise } = useLoaderData() as { dataPromise: Promise<any> };

  return (
    <div>
      <Suspense fallback={<LoadingState />}>
        <Await resolve={dataPromise}>
          <MyChildComponent />
        </Await>
      </Suspense>
    </div>
  );
}

export const MyChildComponent: FC = () => {
  // Then, inside our component that will consume the data returned by the loader (which is wrapped by the Await component)
  // we can access the data of our resolved promise using the useAsyncValue hook.
  const { data } = useAsyncValue() as ApiResponsePayload;

  return (
    <pre>
      {JSON.stringify(data, null, 2)}
    </pre>
  );
}
```

<br>

### Error handling with Async React Router

If we want to show a generic error in case the promise we passed to the `Await` component is rejected because of an error we can use the `errorElement` prop of the `Await` component.

```TSX
export const MyParentComponent: FC = () => {
  // First thing we get the promise produced by the loader function and after setting up a Suspense wrapper
  // we use the Await component provided by React Router to wrap the component that will consume the data.
  const { dataPromise } = useLoaderData() as { dataPromise: Promise<any> };

  return (
    <div>
      <Suspense fallback={<LoadingState />}>
        <Await resolve={dataPromise} errorElement={<ErrorState />}>
          <MyChildComponent />
        </Await>
      </Suspense>
    </div>
  );
}
```

In case we want to execute some specific logic on error or if we need/want to pass the actual error object to our component we can get the error value using the `useAsyncError` hook inside our component.

```TSX
export const MyChildComponent: FC = () => {
  const { data } = useAsyncValue() as ApiResponsePayload;
  const error = useAsyncError();

  if (error) {
    return <ErrorState error={error} />;
  }

  return (
    <pre>
      {JSON.stringify(data, null, 2)}
    </pre>
  );
}
```

<br>

## Lazy Loading with React router

To lazy load components related to specific routes we just need to import our components as shown in previously and add the component to our route/s.

```TS
// Default export
const DefaultExportComponent = React.lazy(() => import('./DefaultExportComponent'));

// Named export
const NamedExportComponent = React.lazy(() =>
  import('./NamedExportComponent').then(module => ({ default: module.NamedExportComponent}))
)
// With named exports we basically need to shape the imported code in the way that React.lazy expects it.
```
