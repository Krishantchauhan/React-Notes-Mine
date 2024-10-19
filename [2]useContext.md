# Todo Context and Counter Component

## Overview

Simple counter application using React Context for state management. The counter can be incremented and decremented with buttons.

## TodoContext

### Code

```javascript
import { createContext, useState } from 'react';

const TodoContext = createContext();

function TodoProvider({ children }) {
  const [count, setCount] = useState(0);

  function inc() {
    setCount(count + 1);
  }

  function dec() {
    setCount(count - 1);
  }

  return <TodoContext.Provider value={{ count, inc, dec }}>{children}</TodoContext.Provider>;
}

export { TodoProvider, TodoContext };
```

### Description

- **createContext**: Creates a new context for the Todo application.
- **useState**: Manages the counter's state.
- **Provider**: Wraps children components with context, providing `count`, `inc`, and `dec` functions.

### Functions

- **inc**: Increments the counter.
- **dec**: Decrements the counter (disabled when count <= 0).

## Counter Component

### Code

```javascript
import { FaPlus, FaMinus } from 'react-icons/fa';
import { useContext } from 'react';
import { TodoContext } from './TodoContext';

function Counter() {
  const { count, inc, dec } = useContext(TodoContext);

  return (
    <div className="flex flex-col items-center justify-center h-[70vh] ">
      <h1 className="text-2xl">Count {count}</h1>
      <div className="flex flex-col mt-4 md:flex-row">
        <button onClick={inc} className="px-7 py-2 border rounded-xl flex justify-center text-xl hover:glow duration-300 md:mx-7 my-8">
          inc
          <FaPlus className="mt-1 mx-3" size={20} />
        </button>
        <button
          onClick={dec}
          disabled={count <= 0}
          className={`px-7 py-2 border rounded-xl flex justify-center text-xl hover:glow duration-300 md:mx-7 md:my-8 ${
            count <= 0 && 'bg-gray-400 cursor-not-allowed'
          }`}
        >
          Dec
          <FaMinus className="mt-1 mx-3" />
        </button>
      </div>
    </div>
  );
}

export default Counter;
```

### Description

- **useContext**: Consumes the `TodoContext`.
- Displays the current `count`.
- Contains two buttons for incrementing and decrementing:
  - **Increment button**: Increases the count and shows a plus icon.
  - **Decrement button**: Decreases the count, disabled if count is zero, and shows a minus icon.

## Usage

Wrap the application with `TodoProvider` to provide context to the `Counter` component.

### Example

```javascript
import React from 'react';
import { TodoProvider } from './TodoContext';
import Counter from './Counter';

function App() {
  return (
    <TodoProvider>
      <Counter />
    </TodoProvider>
  );
}

export default App;
```
