
# Movie List Application 

## 1. MovieList Component Setup

This component is responsible for managing the movie data and rendering the movie posters. It uses React hooks for state management and side effects.

```javascript
import { useState, useEffect } from 'react';
import NavBar from './NavBar'; // Default import
import { motion } from 'framer-motion';

function MovieList() {
  const [movies, setMovies] = useState([]);
  const [inputText, setInputText] = useState('iron man');

  const API_KEY = import.meta.env.VITE_MOVIES_API_KEY;
```

## 2. API Request Function (getMovieReq)

This asynchronous function fetches movie data from the OMDB API based on the user’s input. If the search returns results, it updates the movies state.

```javascript
const getMovieReq = async (inputText) => {
  const url = `https://www.omdbapi.com/?s=${inputText}&apikey=${API_KEY}`;
  const res = await fetch(url);
  const resJSON = await res.json();
  if (resJSON.Search) {
    setMovies(resJSON.Search);
  }
};
```

### Key Points

- **API URL Construction**:
  - Constructs the API URL dynamically.
- **Data Retrieval**:
  - Uses fetch to retrieve data.
- **State Update Check**:
  - Checks for a successful search before updating the state.

## 3. Using useEffect to Fetch Movies

The useEffect hook triggers the getMovieReq function whenever inputText changes, allowing for dynamic searches.

```javascript
useEffect(() => {
  getMovieReq(inputText);
}, [inputText]);
```

### Key Points

- **Data Fetching**:
  - Ensures that the movies are fetched every time the input text is updated.
- **Real-time Updates**:
  - Reacts to changes in user input for real-time searching.

## 4. Rendering the Component

The component renders a sticky NavBar at the top and a grid of movie posters below. The posters are animated using Framer Motion.

```javascript
return (
  <>
    <div>
      <div className="sticky top-0 z-10 mb-2 border border-gray-400 rounded-b-xl">
        <NavBar inputText={inputText} setInputText={setInputText} />
      </div>
      <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 p-4">
        {movies.map((movie) => (
          <motion.div
            key={movie.imdbID}
            className="flex justify-center"
            initial={{ opacity: 0, scale: 0.8 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ duration: 0.2 }}
          >
            <img src={movie.Poster} alt="movie" className="hover:scale-110 duration-200" />
          </motion.div>
        ))}
      </div>
    </div>
  </>
);
```

### Key Points

- **Responsive Design**:
  - Uses CSS classes for a responsive grid layout.
- **Interactivity**:
  - Each movie poster has a hover effect for interactivity.
- **User Experience**:
  - Animated transitions improve user experience.

### 5. NavBar Component

This component provides the user interface for entering the movie search query.

```javascript
import PropTypes from 'prop-types';

function NavBar({ inputText, setInputText }) {
  return (
    <div className="flex justify-between items-center bg-black px-6 py-3 rounded-b-xl">
      <h1 className="text-3xl">MOVIES</h1>
      <div>
        <input
          type="text"
          className="py-2 border rounded-lg pl-2"
          placeholder="Enter to Search"
          value={inputText}
          onChange={(e) => setInputText(e.target.value)}
        />
      </div>
    </div>
  );
}

NavBar.propTypes = {
  inputText: PropTypes.string.isRequired,
  setInputText: PropTypes.func.isRequired,
};

export default NavBar; // Default export
```

### Key Points

- **Props Handling**:
  - Accepts `inputText` and `setInputText` as props for controlled input.
- **UI Elements**:
  - Displays a title and an input field.
- **Prop Validation**:
  - Ensures correct usage of props.
