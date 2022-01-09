### useReducer

incase of complex state management, instead of useSate, will use this  

```
import React, { useReducer } from 'react';
import './style.css';

const initialState = 0;
const countReducer = (state, action) => {
  switch (action) {
    case 'inc':
      return state + 1;
    case 'dec':
      return state - 1;
  }
};

export default function App() {
  const [count, dispatch] = useReducer(countReducer, initialState);
  return (
    <div>
      <h1>Hello StackBlitz!</h1>
      count: {count}
      <br />
      <button onClick={() => dispatch('inc')}>Inc</button>
      <button onClick={() => dispatch('dec')}>Dec</button>
    </div>
  );
}
```
