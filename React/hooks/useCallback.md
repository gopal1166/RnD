### useCallback

Each time child render, updateFun will be re defined, created a new reference  
So prop.setCount will be different on every child render.
```
//import { useState } from 'react';
import React from 'react';
const { useState, useEffect } = React;

export const Counter = () => {
  const [count, setCount] = useState(0);
  const updateFun = () => {
    // setCount(count + 1);
  };
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
      <MyTest setCount={updateFun} />
    </div>
  );
};

const MyTest = (props) => {
  const [count, setCount] = useState(0);
  useEffect(() => {
    setCount((prev) => prev + 1);
  }, [props.setCount]);
  return <div>child:{count}</div>;
};
// ReactDOM.render(<Counter />, document.getElementById('app'));
```