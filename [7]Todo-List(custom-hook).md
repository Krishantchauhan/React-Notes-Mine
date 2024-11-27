
# Todo List Application Using Custom Hook

## 1. TodoList Component Setup

This component manages the todo list functionality, including adding, editing, deleting, and filtering items. It uses a custom hook for state management.

```javascript
import useList from './useList';
import { FaTrash, FaPen } from 'react-icons/fa';

export default function Todolist() {
  const { inputValue, items, getVal, addItem, handleDelete, handleEdit, filterValue, handleFilter } = useList();
```

## 2. Form for Adding Items

The form captures user input and allows users to add new items to the list.

```javascript
  return (
    <>
      <div className="">
        <form className="flex flex-col mt-3 items-center justify-center ">
          <input
            className="border p-2 border-zinc-500 rounded-md w-1/5 max-w-md mx-auto"
            type="text"
            value={inputValue}
            onChange={(e) => getVal(e)}
            placeholder="Enter to add Item"
          />
          <button className="text-black hover:text-white bg-blue-500 mt-3 rounded-xl p-2" onClick={addItem}>
            Add Item
          </button>
        </form>
      </div>
```


## 3. Filter Functionality

An input field for filtering the list of items based on user input.

```javascript
      <div>
        <input type="text" value={filterValue} onChange={handleFilter} placeholder="Filter items" />
      </div>
```

### Key Points

- **Filtering**:
  - Allows users to filter through existing items in real-time.

## 4. Rendering the Todo List

The component maps over the list of items and displays them, along with delete and edit options.

```javascript
      <ul className="flex flex-col items-center justify-center space-y-2 w-full max-w-md mx-auto">
        {items.map((item, index) => (
          <li className="flex items-center justify-between border border-zinc-500 p-2 rounded-md bg-white shadow-md hover:shadow-lg transition-shadow duration-300 w-full" key={index}>
            <span className="text-gray-800">{item}</span>
            <div className="flex space-x-2">
              <FaTrash onClick={() => handleDelete(index)} className="text-red-500 cursor-pointer hover:text-red-700 transition-colors hover:scale-125 duration-700" />
              <FaPen onClick={() => handleEdit(index)} className="text-blue-500 cursor-pointer hover:text-blue-700 transition-colors hover:scale-125 duration-700" />
            </div>
          </li>
        ))}
      </ul>
```

### Key Points

- **Dynamic Rendering**:
  - Each item is displayed with edit and delete options.
- **Styling and Effects**:
  - Styled for interactivity with hover effects.

## 5. useList Hook

This custom hook encapsulates all logic related to managing the todo list.

```javascript
import { useState } from 'react';

export default function useList() {
  const [inputValue, setInputValue] = useState('');
  const [filterValue, setFilterValue] = useState('');
  const [items, setItems] = useState([]);
  const [isEditing, setIsEditing] = useState(false);
  const [editIndex, setEditIndex] = useState(null);
```

### Key Points

- **State Management**:
  - Manages state for input values, filter values, and items.

## 6. Function Definitions

### a. getVal

Updates the input value from the input field.

```javascript
  function getVal(e) {
    setInputValue(e.target.value);
  }
```

### b. addItem

Adds a new item or updates an existing one based on the editing state.

```javascript
  function addItem(e) {
    e.preventDefault();
    if (inputValue !== null) {
      if (isEditing) {
        const updatedItems = [...items];
        updatedItems[editIndex] = inputValue;
        setItems(updatedItems);
        setIsEditing(false);
        setEditIndex(null);
      } else {
        setItems([...items, inputValue]);
      }
    }
    setInputValue('');
  }
```

### c. handleDelete

Removes an item from the list by its index.

```javascript
  function handleDelete(key) {
    setItems(items.filter((item, index) => index !== key));
  }
```

### d. handleEdit

Prepares to edit an item by setting the input value and index.

```javascript
  function handleEdit(key) {
    setInputValue(items[key]);
    setEditIndex(key);
    setIsEditing(true);
  }
```

### e. handleFilter

Updates the filter value based on user input.

```javascript
  function handleFilter(e) {
    const search = e.target.value;
    setFilterValue(search);
  }
```

### f. Filtered Items

Filters the items based on the current filter input.

```javascript
  const filteredItems = items.filter((item) => item.toLowerCase().includes(filterValue.toLowerCase()));
```
### e. Return
```javascript
return { inputValue, items: filteredItems, getVal, addItem, handleDelete, handleEdit, filterValue, handleFilter };
```