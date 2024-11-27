# Arrays Component and useArray Hook

This document outlines the `Arrays` component that utilizes a custom `useArray` hook to manage an array with various operations.

## Arrays Component

The `Arrays` component displays an array and provides buttons to manipulate the array through various actions.

### Code Implementation

```javascript
import { useArray } from './useArray';

const INITIAL_ARRAY = [1, 2, 3];

const Arrays = () => {
  const { array, set, push, replace, filter, remove, clear, reset } = useArray(INITIAL_ARRAY);

  return (
    <>
      <div>{array.join(', ')}</div>
      <div
        style={{
          display: 'flex',
          flexDirection: 'column',
          gap: '.5rem',
          alignItems: 'flex-start',
          marginTop: '1rem',
        }}
      >
        <button onClick={() => set([4, 5, 6])}>Set to [4, 5, 6]</button>
        <button onClick={() => push(4)}>Push 4</button>
        <button onClick={() => replace(1, 9)}>Replace the second element with 9</button>
        <button onClick={() => filter((n) => n < 3)}>Keep numbers less than 3</button>
        <button onClick={() => remove(1)}>Remove second element</button>
        <button onClick={clear}>Clear</button>
        <button onClick={reset}>Reset</button>
      </div>
    </>
  );
};

export default Arrays;
```

### Key Features

- Displays the current array as a comma-separated string.
- Provides buttons for:
  - Setting the array to a new value.
  - Pushing new elements.
  - Replacing elements at specific indices.
  - Filtering elements based on a condition.
  - Removing elements.
  - Clearing the array.
  - Resetting the array to its initial state.

## useArray Hook

The `useArray` hook encapsulates the logic for managing an array and provides methods to manipulate it.

### Code Implementation

```javascript
import { useState } from 'react';

export function useArray(INITIAL_ARRAY) {
  const [array, setArray] = useState(INITIAL_ARRAY);

  function push(element) {
    setArray([...array, element]);
  }

  function replace(idx, element) {
    setArray([...array.slice(0, idx), element, ...array.slice(idx + 1)]);
  }

  function filter(callback) {
    setArray(array.filter(callback));
  }

  function remove(idx) {
    setArray([...array.slice(0, idx), ...array.slice(idx + 1)]);
  }

  function clear() {
    setArray([]);
  }

  function reset() {
    setArray(INITIAL_ARRAY);
  }

  return { array, set: setArray, push, replace, filter, remove, clear, reset };
}
```

### Key Features

- **State Management:** Uses the `useState` hook to maintain the current array.
- **Array Manipulation Functions:**
  - `push(element)`: Adds a new element to the end of the array.
  - `replace(idx, element)`: Replaces the element at the specified index with a new element.
  - `filter(callback)`: Filters the array based on a callback function.
  - `remove(idx)`: Removes the element at the specified index.
  - `clear()`: Clears the array.
  - `reset()`: Resets the array to its initial state.

## Summary

The `Arrays` component and the `useArray` hook provide a comprehensive way to manage and manipulate arrays in a React application, making it easy to perform common operations.
