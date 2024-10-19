# Calculator Application

---

> # All of the Calculation is separated

> ## Summary
>
> - **Main Calculator Component**: Manages the state and passes values to child components.
> - **Sum, Sub, Multiply Components**: Each performs a specific mathematical operation and updates the result. Uses `react-icons` for visually interactive buttons.

---

## 1. Calculator Component

This is the main component that handles user input and displays the result. It manages the state for `number1`, `number2`, and the `result` using React's `useState` hook.

```javascript
import React, { useState } from 'react';
import Sum from './Sum';
import Sub from './Sub';
import Multiply from './Multiply';

function Calculator() {
  const [result, setResult] = useState(0);
  const [number1, setNumber1] = useState(0);
  const [number2, setNumber2] = useState(0);
  return (
    <>
      <div>
        <h1>Result :- {result} </h1>
        <input type="number" value={number1} onChange={(e) => setNumber1(parseFloat(e.target.value))} placeholder="Enter first number" />
        <input type="number" value={number2} onChange={(e) => setNumber2(parseFloat(e.target.value))} placeholder="Enter Second number" />
      </div>
      <div>
        <Sum number1={number1} number2={number2} setResult={setResult} />
        <Sub number1={number1} number2={number2} setResult={setResult} />
        <Multiply number1={number1} number2={number2} setResult={setResult} />
      </div>
    </>
  );
}

export default Calculator;
```

**Key Points**

- **State Management**: Uses `useState` to track `number1`, `number2`, and `result`.
- **Input Handling**: Parses and sets the user’s input as floating point numbers.
- **Child Components**: Renders three buttons for adding, subtracting, and multiplying numbers, each using separate components.

---

## 2. Sum Component

This component handles the addition of the two numbers. It uses the `FaPlus` icon from `react-icons` for the add button.

```javascript
import { FaPlus } from 'react-icons/fa';

function Sum({ number1, number2, setResult }) {
  const doAdd = () => {
    const sum = number1 + number2;
    setResult(sum);
  };
  return (
    <>
      <button onClick={doAdd}>
        <FaPlus />
      </button>
    </>
  );
}

export default Sum;
```

**Key Points**

- **Addition Logic**: Adds `number1` and `number2`, then updates the `result` state.
- **Button Icon**: Displays a plus icon (`FaPlus`) from `react-icons`.

---

## 3. Sub Component

This component handles the subtraction operation. It displays a minus button using `FaMinus` from `react-icons`.

```javascript
import { FaMinus } from 'react-icons/fa';

function Sub({ number1, number2, setResult }) {
  const doSub = () => {
    const sum = number1 - number2;
    setResult(sum);
  };
  return (
    <>
      <button onClick={doSub}>
        <FaMinus />
      </button>
    </>
  );
}

export default Sub;
```

**Key Points**

- **Subtraction Logic**: Subtracts `number2` from `number1` and sets the `result`.
- **Button Icon**: Displays a minus icon (`FaMinus`) for subtraction.

---

## 4. Multiply Component

This component handles multiplication and displays a multiplication icon (`FaTimes` from `react-icons`) for the operation.

```javascript
import { FaTimes } from 'react-icons/fa';

function Multiply({ number1, number2, setResult }) {
  const doMul = () => {
    const mul = number1 * number2;
    setResult(mul);
  };
  return (
    <>
      <button onClick={doMul}>
        <FaTimes />
      </button>
    </>
  );
}

export default Multiply;
```

**Key Points**

- **Multiplication Logic**: Multiplies `number1` and `number2`, then updates the `result` state.
- **Button Icon**: Uses the `FaTimes` icon from `react-icons` for multiplication.

---
