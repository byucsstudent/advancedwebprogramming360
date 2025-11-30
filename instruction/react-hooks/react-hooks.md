# React Hooks

## Overview

React Hooks, introduced in React 16.8, revolutionized how we write React components. Before hooks, managing state and side effects in functional components was cumbersome, often requiring conversion to class components. Hooks provide a way to "hook into" React state and lifecycle features from functional components, making code cleaner, more reusable, and easier to understand. This module will guide you through understanding, implementing, and utilizing React Hooks effectively. We will explore their benefits, limitations, internal workings, and best practices.

## Learning Objectives

By the end of this module, you will be able to:

*   Explain the motivation behind React Hooks and their benefits over class components.
*   Describe the fundamental principles behind how React Hooks work.
*   Implement and use the built-in React Hooks: `useState`, `useEffect`, `useContext`, `useReducer`, `useCallback`, `useMemo`, and `useRef`.
*   Create custom React Hooks to encapsulate reusable logic.
*   Identify common pitfalls and anti-patterns when using React Hooks.
*   Apply best practices for writing clean and maintainable code with React Hooks.
*   Understand the internal workings of React Hooks with a simplified implementation.

## Key Concepts

*   **Functional Components:**  Hooks are designed to be used within functional components.
*   **State Management:**  Hooks provide a way to manage component state within functional components.
*   **Side Effects:** Hooks allow you to perform side effects, such as data fetching, subscriptions, and manual DOM manipulations.
*   **Reusability:** Custom Hooks enable you to extract and reuse stateful logic across multiple components.
*   **Rules of Hooks:** Hooks must be called at the top level of a React function and only from React function components or custom Hooks.

## Why React Hooks? (The Problem They Solve)

Before hooks, React developers faced challenges like:

*   **Complex Component Logic:**  Sharing stateful logic between components was difficult, often leading to complex render props and higher-order components.  This made code harder to read and maintain.
*   **Class Component Boilerplate:** Class components required a significant amount of boilerplate code, making them less concise than functional components. The `this` keyword also presented potential pitfalls.
*   **Difficulty in Reusing Logic:**  There was no straightforward way to reuse stateful logic across components without resorting to complex patterns.

Hooks address these issues by:

*   **Simplifying State Management:** Providing a direct way to manage state in functional components.
*   **Promoting Code Reusability:** Enabling the creation of custom hooks to share stateful logic.
*   **Reducing Boilerplate:**  Making functional components more concise and easier to understand.

## Built-in React Hooks

React provides several built-in hooks to cover common use cases.

### `useState`

The `useState` hook allows you to add state to functional components.

**Syntax:**

```javascript
const [state, setState] = useState(initialState);
```

*   `state`: The current state value.
*   `setState`: A function to update the state.
*   `initialState`: The initial value of the state.

**Example:**

```javascript
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
}

export default Counter;
```

**Explanation:**

This example creates a simple counter component. `useState(0)` initializes the `count` state to 0. The `setCount` function is used to update the `count` state when the "Increment" or "Decrement" buttons are clicked. The component re-renders whenever the `count` state changes.

### `useEffect`

The `useEffect` hook allows you to perform side effects in functional components.  Side effects include data fetching, subscriptions, manual DOM manipulations, and more.

**Syntax:**

```javascript
useEffect(() => {
  // Code to run after render
  return () => {
    // Optional cleanup function
  };
}, [dependencies]);
```

*   `callback`: A function containing the side effect logic.
*   `dependencies`: An optional array of dependencies. The effect will only run if any of the dependencies have changed since the last render. If the array is empty (`[]`), the effect will only run once after the initial render. If the array is omitted, the effect will run after every render.
*   `cleanup function`: An optional function that runs when the component unmounts or before the effect re-runs due to a change in dependencies.  This is useful for cleaning up resources like subscriptions or timers.

**Example:**

```javascript
import React, { useState, useEffect } from 'react';

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    async function fetchData() {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
      const json = await response.json();
      setData(json);
    }

    fetchData();

    return () => {
      // Cleanup function (optional) - e.g., cancel a network request
      console.log("Component unmounted or effect re-running");
    };
  }, []); // Empty dependency array means this effect runs only once after initial render

  if (!data) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      <h1>Data from API</h1>
      <p>Title: {data.title}</p>
    </div>
  );
}

export default DataFetcher;
```

**Explanation:**

This example fetches data from an API endpoint using `useEffect`. The empty dependency array (`[]`) ensures that the effect runs only once after the initial render. The cleanup function is optional but can be used to prevent memory leaks by canceling the network request if the component unmounts before the data is fetched.

### `useContext`

The `useContext` hook allows you to consume values from a React context.

**Syntax:**

```javascript
const value = useContext(MyContext);
```

*   `MyContext`: The context object created using `React.createContext`.
*   `value`: The current context value.

**Example:**

```javascript
import React, { createContext, useContext } from 'react';

// Create a context
const ThemeContext = createContext('light');

function ThemedComponent() {
  const theme = useContext(ThemeContext);

  return (
    <div style={{ backgroundColor: theme === 'light' ? '#fff' : '#333', color: theme === 'light' ? '#000' : '#fff' }}>
      <p>Current Theme: {theme}</p>
    </div>
  );
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedComponent />
    </ThemeContext.Provider>
  );
}

export default App;
```

**Explanation:**

This example creates a `ThemeContext` and provides a value of "dark" to it within the `App` component. The `ThemedComponent` uses `useContext` to access the current theme value and applies styles accordingly.

### `useReducer`

The `useReducer` hook is an alternative to `useState` for managing more complex state logic. It's similar to Redux's reducer concept.

**Syntax:**

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

*   `reducer`: A function that takes the current state and an action as arguments and returns the new state.
*   `initialArg`: The initial state value.
*   `init`: An optional initializer function that allows you to lazily initialize the state.
*   `state`: The current state value.
*   `dispatch`: A function to dispatch actions to the reducer.

**Example:**

```javascript
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}

export default Counter;
```

**Explanation:**

This example uses `useReducer` to manage the `count` state. The `reducer` function handles `increment` and `decrement` actions. The `dispatch` function is used to send actions to the reducer.

### `useCallback`

The `useCallback` hook memoizes a function. It returns a memoized version of the callback that only changes if one of the dependencies has changed. This is useful for optimizing performance by preventing unnecessary re-renders of child components that receive the callback as a prop.

**Syntax:**

```javascript
const memoizedCallback = useCallback(
  () => {
    // Function logic
  },
  [dependencies],
);
```

*   `callback`: The function to memoize.
*   `dependencies`: An array of dependencies. The callback will only be recreated if one of the dependencies has changed.

**Example:**

```javascript
import React, { useState, useCallback } from 'react';

function ChildComponent({ onClick }) {
  console.log("Child Component Rendered");
  return <button onClick={onClick}>Click Me</button>;
}

function ParentComponent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount(c => c + 1);
  }, []); // Empty dependency array - this function will never be recreated

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}

export default ParentComponent;
```

**Explanation:**

In this example, `useCallback` ensures that the `handleClick` function is only created once. Without `useCallback`, the `handleClick` function would be recreated on every render of `ParentComponent`, potentially causing `ChildComponent` to re-render unnecessarily. The `console.log` inside `ChildComponent` will only be printed once, illustrating the memoization.

### `useMemo`

The `useMemo` hook memoizes a value. It returns a memoized value that only changes if one of the dependencies has changed. This is useful for optimizing performance by preventing expensive calculations from being re-executed unnecessarily.

**Syntax:**

```javascript
const memoizedValue = useMemo(
  () => {
    // Calculation logic
    return computedValue;
  },
  [dependencies],
);
```

*   `callback`: A function that performs the calculation.
*   `dependencies`: An array of dependencies. The value will only be recalculated if one of the dependencies has changed.

**Example:**

```javascript
import React, { useState, useMemo } from 'react';

function ExpensiveComponent({ data }) {
  // Simulate an expensive calculation
  const processedData = useMemo(() => {
    console.log("Processing data...");
    // Imagine this is a very complex operation
    return data.map(item => item * 2);
  }, [data]);

  return (
    <div>
      <p>Processed Data: {processedData.join(', ')}</p>
    </div>
  );
}

function App() {
  const [number, setNumber] = useState(1);
  const data = [number, number + 1, number + 2];

  return (
    <div>
      <button onClick={() => setNumber(number + 1)}>Increment Number</button>
      <ExpensiveComponent data={data} />
    </div>
  );
}

export default App;
```

**Explanation:**

In this example, `useMemo` memoizes the `processedData` value. The `console.log` statement inside the `useMemo` callback will only be executed when the `data` prop changes. This prevents the expensive calculation from being re-executed unnecessarily when the parent component re-renders for other reasons.

### `useRef`

The `useRef` hook provides a way to create a mutable reference that persists across renders. It's commonly used to access DOM elements directly or to store values that don't trigger re-renders when they change.

**Syntax:**

```javascript
const refContainer = useRef(initialValue);
```

*   `initialValue`: The initial value of the reference.
*   `refContainer.current`: The current value of the reference.

**Example:**

```javascript
import React, { useRef, useEffect } from 'react';

function FocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    // Focus the input element on initial render
    inputRef.current.focus();
  }, []);

  return (
    <div>
      <input type="text" ref={inputRef} />
    </div>
  );
}

export default FocusInput;
```

**Explanation:**

This example uses `useRef` to create a reference to the input element. The `useEffect` hook is used to focus the input element after the initial render.

## Custom Hooks

Custom Hooks are JavaScript functions that start with "use" and can call other Hooks. They allow you to extract reusable stateful logic from components.

**Example:**

```javascript
import { useState, useEffect } from 'react';

function useWindowSize() {
  const [windowSize, setWindowSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight,
  });

  useEffect(() => {
    function handleResize() {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight,
      });
    }

    window.addEventListener('resize', handleResize);

    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return windowSize;
}

export default useWindowSize;

// Usage in a component:
import React from 'react';
import useWindowSize from './useWindowSize';

function MyComponent() {
  const windowSize = useWindowSize();

  return (
    <div>
      <p>Window Width: {windowSize.width}</p>
      <p>Window Height: {windowSize.height}</p>
    </div>
  );
}

export default MyComponent;
```

**Explanation:**

This example creates a custom hook called `useWindowSize` that tracks the window's width and height. The hook uses `useState` to store the window size and `useEffect` to listen for resize events. The hook returns the current window size. This hook can then be used in any component that needs to know the window size.

## How React Hooks Work (Simplified Implementation)

Understanding how React Hooks work internally can provide valuable insights into their behavior and limitations.  Here's a simplified illustration:

```javascript
// A very simplified example - doesn't cover all edge cases
let hookStates = []; // Array to store state for each hook
let hookIndex = 0;    // Index to track the current hook

function useState(initialState) {
  const currentIndex = hookIndex; // Capture the current hook index
  hookIndex++; // Increment for the next hook call

  if (hookStates[currentIndex] === undefined) {
    hookStates[currentIndex] = initialState; // Initialize if not already
  }

  const setState = (newState) => {
    hookStates[currentIndex] = newState;
    // Ideally trigger a re-render here - omitted for simplicity
    console.log("State updated. New state:", newState);
  };

  return [hookStates[currentIndex], setState];
}

// Example usage (inside a functional component):
function MyComponent() {
  hookIndex = 0; // Reset hook index before each render

  const [count, setCount] = useState(0);
  const [text, setText] = useState("Initial Text");

  return `
    <div>
      <p>Count: ${count}</p>
      <button onclick="setCount(count + 1)">Increment</button>
      <p>Text: ${text}</p>
      <input type="text" value="${text}" onchange="setText(event.target.value)" />
    </div>
  `;
}

// Simulate a render:
console.log(MyComponent());
```

**Explanation:**

1.  **State Storage:** The `hookStates` array stores the state for each hook used in a component.
2.  **Hook Index:** The `hookIndex` variable keeps track of the order in which hooks are called during each render.
3.  **`useState` Implementation:** The `useState` function retrieves the state value from the `hookStates` array based on the current `hookIndex`. It also provides a `setState` function to update the state.
4.  **Order Matters:** Hooks rely on being called in the same order during each render.  This is why they must be called at the top level of a functional component and not inside loops, conditions, or nested functions.
5.  **Re-renders:**  The `setState` function (in a real React implementation) would trigger a re-render of the component, causing the `MyComponent` function to be called again, and the hooks to be re-executed in the same order, retrieving their updated state from the `hookStates` array.  This re-rendering is omitted for simplicity in the example.
