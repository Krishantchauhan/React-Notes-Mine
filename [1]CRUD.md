# CRUD App with LocalStorage - Key Points

### 1. **State Management with `useState`**
   - **inputText**: Stores the input value from the user.
   - **items**: Holds the list of items displayed in the app.
   - **isEditing**: A boolean to track whether the user is editing an existing item.
   - **idx**: Holds the index of the item currently being edited.

   ```js
   const [inputText, setInputText] = useState('');
   const [items, setItems] = useState([]);
   const [isEditing, setIsEditing] = useState(false);
   const [idx, setIdx] = useState(null);
   ```

### 2. **Loading Saved Items from LocalStorage (useEffect)**
   - On component mount, items are loaded from `localStorage` to persist data across page reloads.
   
   ```js
   useEffect(() => {
     const savedItems = JSON.parse(localStorage.getItem('items')) || [];
     setItems(savedItems);
   }, []);
   ```

### 3. **Adding/Editing an Item (`addItem`)**
   - **Add**: Adds the new item to the list.
   - **Edit**: Updates the existing item in the list when in edit mode.

   ```js
   function addItem() {
     if (isEditing) {
       const updatedItems = [...items];
       updatedItems[idx] = inputText;
       setItems(updatedItems);
       setIsEditing(false);
       setIdx(null);
       addToLocal(updatedItems);
     } else {
       const newItems = [...items, inputText];
       setItems(newItems);
       addToLocal([...items, inputText]);
     }
     setInputText('');
   }
   ```

### 4. **Saving Items to LocalStorage (`addToLocal`)**
   - Stores the current list of items in `localStorage` in JSON format.

   ```js
   function addToLocal(inputText) {
     localStorage.setItem('items', JSON.stringify(inputText));
   }
   ```

### 5. **Deleting an Item (`delItem`)**
   - Removes an item from the list based on the index, and updates `localStorage`.

   ```js
   function delItem(index) {
     const newItems = items.filter((_, idx) => idx !== index);
     setItems(newItems);
     addToLocal(newItems);
   }
   ```

### 6. **Editing an Item (`editItem`)**
   - Switches the app to edit mode, allowing the user to modify an existing item.

   ```js
   function editItem(index) {
     setIsEditing(true);
     setInputText(items[index]);
     setIdx(index);
   }
   ```

Here's the final part of your code, focusing on the `return` section inside the `App` component:

```js
return (
  <>
    <div>
      <input
        type="text"
        value={inputText}
        onChange={(e) => setInputText(e.target.value)}
      /> 
      <button onClick={addItem}>ADD</button>
    </div>

    <div>
      <ol>
        //Display
        {items.map((item, index) => (
          <li key={index}>
            {item}
            <FaTrash onClick={() => delItem(index)} />
            <FaPen onClick={() => editItem(index)} />
          </li>
        ))}

      </ol>
    </div>
  </>
);
```
