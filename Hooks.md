Sure! Here is a detailed list of common React hooks with examples.

---

### 1. **useState**

The `useState` hook is used to declare state variables in functional components.

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
}

export default Counter;
```

### 2. **useEffect**

The `useEffect` hook allows you to perform side effects in your components, such as fetching data, manipulating the DOM, or setting up subscriptions.

```jsx
import React, { useState, useEffect } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => setData(data));
  }, []);  // Empty array means this runs once after the initial render

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : <p>Loading...</p>}
    </div>
  );
}

export default DataFetcher;
```

### 3. **useContext**

The `useContext` hook is used to access the context value in functional components.

```jsx
import React, { useContext, useState, createContext } from 'react';

// Create Context
const MyContext = createContext();

// Provider Component
const MyProvider = ({ children }) => {
  const [state, setState] = useState("Hello from Context");
  return <MyContext.Provider value={{ state, setState }}>{children}</MyContext.Provider>;
};

// Consumer Component
const Display = () => {
  const { state } = useContext(MyContext);
  return <h1>{state}</h1>;
};

const App = () => {
  return (
    <MyProvider>
      <Display />
    </MyProvider>
  );
};

export default App;
```

### 4. **useReducer**

`useReducer` is an alternative to `useState` that is more suitable for managing complex state logic in functional components.

```jsx
import React, { useReducer } from 'react';

const initialState = { count: 0 };

const reducer = (state, action) => {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h2>Count: {state.count}</h2>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
};

export default Counter;
```

### 5. **useRef**

`useRef` is used to persist values between renders without causing a re-render. It can also be used to access DOM elements directly.

```jsx
import React, { useRef } from 'react';

const FocusInput = () => {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
};

export default FocusInput;
```

### 6. **useMemo**

The `useMemo` hook memoizes expensive function calls and prevents unnecessary recalculations unless the dependencies change.

```jsx
import React, { useState, useMemo } from 'react';

const ExpensiveComputation = ({ num }) => {
  const computeFactorial = (n) => {
    console.log("Calculating factorial...");
    return n <= 0 ? 1 : n * computeFactorial(n - 1);
  };

  const factorial = useMemo(() => computeFactorial(num), [num]);

  return <p>Factorial of {num} is {factorial}</p>;
};

const App = () => {
  const [num, setNum] = useState(5);

  return (
    <div>
      <ExpensiveComputation num={num} />
      <button onClick={() => setNum(num + 1)}>Increase number</button>
    </div>
  );
};

export default App;
```

### 7. **useCallback**

`useCallback` returns a memoized version of a callback function, which is useful when passing functions to optimized child components.

```jsx
import React, { useState, useCallback } from 'react';

const Button = React.memo(({ onClick }) => {
  console.log('Rendering Button...');
  return <button onClick={onClick}>Click Me</button>;
});

const App = () => {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <Button onClick={increment} />
      <h2>Count: {count}</h2>
    </div>
  );
};

export default App;
```

### 8. **useLayoutEffect**

The `useLayoutEffect` hook works similarly to `useEffect` but is called synchronously after all DOM mutations. This makes it useful for measuring DOM elements before the browser repaints.

```jsx
import React, { useState, useLayoutEffect, useRef } from 'react';

const LayoutEffectExample = () => {
  const [width, setWidth] = useState(0);
  const divRef = useRef(null);

  useLayoutEffect(() => {
    setWidth(divRef.current.offsetWidth);
  }, []);

  return (
    <div>
      <div ref={divRef} style={{ width: '50%' }}>Resize me!</div>
      <p>Width of the div: {width}px</p>
    </div>
  );
};

export default LayoutEffectExample;
```

### 9. **useImperativeHandle**

The `useImperativeHandle` hook customizes the instance value that is exposed when using `ref` in a parent component.

```jsx
import React, { useState, useImperativeHandle, forwardRef } from 'react';

const MyInput = forwardRef((props, ref) => {
  const [value, setValue] = useState('');

  useImperativeHandle(ref, () => ({
    reset: () => setValue('')
  }));

  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
});

const App = () => {
  const inputRef = React.useRef(null);

  const resetInput = () => {
    inputRef.current.reset();
  };

  return (
    <div>
      <MyInput ref={inputRef} />
      <button onClick={resetInput}>Reset Input</button>
    </div>
  );
};

export default App;
```

### 10. **useDebugValue**

The `useDebugValue` hook is used for debugging custom hooks. It displays a label in the React DevTools when inspecting hooks.

```jsx
import React, { useState, useDebugValue } from 'react';

const useCustomHook = () => {
  const [state, setState] = useState("Hello");

  useDebugValue(state);

  return [state, setState];
};

const App = () => {
  const [state, setState] = useCustomHook();

  return <div>{state}</div>;
};

export default App;
```

---

### Summary of Hooks:

1. **useState**: For managing state in functional components.
2. **useEffect**: For side effects like fetching data or DOM manipulation.
3. **useContext**: For accessing context values.
4. **useReducer**: For managing complex state logic with reducers.
5. **useRef**: For persisting values across renders or accessing DOM elements.
6. **useMemo**: For memoizing expensive calculations.
7. **useCallback**: For memoizing functions passed as props.
8. **useLayoutEffect**: For DOM measurements before the browser repaints.
9. **useImperativeHandle**: For customizing instance values exposed to parent components.
10. **useDebugValue**: For debugging custom hooks.

---

These hooks make React functional components more powerful and flexible, allowing you to manage state, side effects, and more in a clean and efficient way.
