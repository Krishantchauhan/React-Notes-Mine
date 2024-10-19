> # Fetch API

---

# User Component

This component fetches and displays a list of users from the JSONPlaceholder API.

## Key Features

- **State Management:** Uses the `useState` hook to manage the `users` state.
- **Data Fetching:** Uses the `useEffect` hook to fetch data from the API when the component mounts.
- **Rendering:** Maps over the `users` array to display each user's name in a list.

## Code Implementation

```javascript
import { useEffect, useState } from 'react';

export default function User() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then((res) => res.json())
      .then(setUsers);
  }, []); // Ensure the empty dependency array is in the correct position

  return (
    <>
      <h1>List of Users</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
}
```

## Key Points

- **`useState` Hook:** Initializes the `users` state to an empty array.
- **`useEffect` Hook:** Fetches data from the API when the component mounts and updates the `users` state with the fetched data.
- **Rendering Logic:** Displays a heading and a list of user names. Each user name is rendered as a list item with a unique key based on the user’s ID.

## Summary

This component effectively demonstrates how to fetch and display data from an external API in a React application using hooks.
