# Todo List Application

## 1. **App Component**

This is the main component that sets up the context provider and renders the Todo component.

```javascript
import './styles.css';
import { TodolistProvider } from './context/TodolistProvider';
import Todo from './components/Todo';

export default function App() {
  return (
    <TodolistProvider>
      <div className="App">
        <Todo />
      </div>
    </TodolistProvider>
  );
}
```

### Key Points

- **Context Provider**: Wraps the `Todo` component in the `TodolistProvider` to allow access to the todo list context.
- **Styling**: Imports the CSS file for styling.

---

## 2. **TodolistProvider Component**

This component manages the state of the todo list using the Context API. It provides methods to add and delete items.

```javascript
import React, { createContext, useState } from 'react';
const TodolistContext = createContext();

function TodolistProvider({ children }) {
  const [input, setInput] = useState('');
  const [items, setItems] = useState([]);

  const addItem = () => {
    if (input.trim() !== '') {
      setItems([...items, input]);
      setInput('');
    }
  };

  const deleteItem = (index) => {
    const newItems = items.filter((_, i) => i !== index);
    setItems(newItems);
  };

  const handleKey = (e) => {
    if (e.key === 'Enter') addItem();
  };

  const getInput = (e) => setInput(e.target.value);

  return;
  <TodolistContext.Provider value={{ input, getInput, addItem, items, deleteItem, handleKey }}>{children}</TodolistContext.Provider>;
}

export { TodolistContext, TodolistProvider };
```

### Key Points

- **State Management**: Uses `useState` to manage the input text and the list of items.
- **Add Item**: The `addItem` function adds a new item to the list if the input is not empty.
- **Delete Item**: The `deleteItem` function removes an item from the list based on its index.
- **Keyboard Handling**: The `handleKey` function allows adding an item by pressing the "Enter" key.
- **Input Handling**: The `getInput` function updates the input state as the user types.

---

## 3. **Todo Component**

This component displays the input field, the add button, and the list of todo items.

```javascript
import React from 'react';
import { TodolistContext } from '../context/TodolistProvider';
import { useContext } from 'react';
import { FaTrash } from 'react-icons/fa';

function Todo() {
  const { getInput, input, addItem, items, deleteItem, handleKey } = useContext(TodolistContext);
  return (
    <>
      <div>
        <input type="text" value={input} onChange={getInput} onKeyDown={handleKey} />
        <button onClick={addItem}>Add</button>
      </div>
      <div>
        <ul>
          {items.map((item, index) => (
            <li key={index}>
              {item}
              <button onClick={() => deleteItem(index)}>
                <FaTrash style={{ color: 'purple' }} />
              </button>
            </li>
          ))}
        </ul>
      </div>
    </>
  );
}

export default Todo;
```

### Key Points

- **Input Field**: Renders an input field that binds to the `input` state.
- **Add Button**: Calls the `addItem` function when clicked.
- **Todo List**: Displays a list of items using `map`, where each item has a delete button.
- **Delete Button**: Calls the `deleteItem` function to remove an item when clicked, using the `FaTrash` icon for visual representation.

---

## Summary

- **Context API**: The application uses the Context API to manage the state of the todo list efficiently.
- **Functional Components**: Implements functional components for clarity and reusability.
- **User Interaction**: Supports user interaction through input fields and buttons, providing a simple interface for managing todos.
