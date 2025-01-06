### React Theory Notes with Examples

React is a powerful JavaScript library used for building user interfaces, especially single-page applications (SPAs). React allows developers to create reusable components, manage the state of applications efficiently, and use the virtual DOM for faster rendering.

Here is a comprehensive theory and code walkthrough for React:

---

## 1. **What is React?**
React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It allows you to build components that manage their state and can be reused across the application.

### Key Concepts in React:
- **Components**: The building blocks of a React application.
- **State**: The data that can change and affect the rendering of a component.
- **Props**: Data passed from a parent component to a child component.
- **JSX**: JavaScript XML, a syntax extension for JavaScript that allows you to write HTML in JavaScript.
- **Virtual DOM**: A lightweight copy of the actual DOM, used for faster rendering and updates.

---

## 2. **Setting Up React Environment**

To start with React, you can set up a new project using **Create React App** or manually using a bundler like Webpack.

To set up React using Create React App:
```bash
npx create-react-app my-app
cd my-app
npm start
```

This will create a new React app and start a local server where you can see your application running.

---

## 3. **React Components**

### Functional Components
Functional components are JavaScript functions that return JSX (HTML-like syntax) and represent parts of the UI.

```jsx
import React from 'react';

// A simple functional component
const Welcome = (props) => {
  return <h1>Hello, {props.name}!</h1>;
}

export default Welcome;
```

**Usage**:
```jsx
<Welcome name="John" />
```

### Class Components
Class components are ES6 classes that extend `React.Component`. They are useful when you need more features like lifecycle methods or state management.

```jsx
import React, { Component } from 'react';

// A class component
class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default Welcome;
```

**Usage**:
```jsx
<Welcome name="John" />
```

---

## 4. **JSX (JavaScript XML)**

JSX is a syntax extension for JavaScript, which allows you to write HTML-like code inside JavaScript. It is used in React to define the structure of the UI.

```jsx
import React from 'react';

// JSX inside a functional component
const App = () => {
  return (
    <div>
      <h1>Welcome to React!</h1>
      <p>This is a JSX example.</p>
    </div>
  );
}

export default App;
```

**Important points about JSX**:
- JSX is compiled to `React.createElement()` calls.
- It is not HTML. For example, `class` in HTML becomes `className` in JSX, and `for` becomes `htmlFor`.
- You can embed JavaScript expressions inside JSX by wrapping them in curly braces `{}`.

```jsx
const name = "John";
const element = <h1>Hello, {name}!</h1>;
```

---

## 5. **Props (Properties)**

Props are used to pass data from a parent component to a child component. They are read-only and allow you to make components dynamic.

```jsx
// Parent Component
import React from 'react';
import Welcome from './Welcome';

const App = () => {
  return <Welcome name="John" />;
}

export default App;

// Child Component
const Welcome = (props) => {
  return <h1>Hello, {props.name}!</h1>;
}
```

### Default Props
You can define default values for props in case they are not passed.

```jsx
Welcome.defaultProps = {
  name: "Guest"
};
```

---

## 6. **State**

State is used to store data that can change over time and cause the component to re-render when the state changes. It is mutable and can be changed using the `setState` method in class components or the `useState` hook in functional components.

### Using State in Functional Components with `useState`

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);  // useState hook
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click Me</button>
    </div>
  );
}

export default Counter;
```

### Using State in Class Components

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };  // Initial state
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={this.increment}>Click Me</button>
      </div>
    );
  }
}

export default Counter;
```

---

## 7. **Event Handling**

React allows you to handle events like clicks, form submissions, and key presses using event handlers. The syntax for event handling is slightly different from regular JavaScript.

```jsx
import React from 'react';

const Button = () => {
  const handleClick = () => {
    alert("Button clicked!");
  };

  return (
    <button onClick={handleClick}>Click Me</button>
  );
}

export default Button;
```

---

## 8. **Conditional Rendering**

In React, you can conditionally render UI elements using JavaScript operators like `if`, `&&`, or ternary (`? :`) operators.

```jsx
import React from 'react';

const Greeting = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please log in</h1>}
    </div>
  );
}

export default Greeting;
```

---

## 9. **Lists and Keys**

You can render lists in React using the `map()` function, and each list item should have a unique `key` prop to help React optimize the re-rendering process.

```jsx
import React from 'react';

const List = () => {
  const items = ["Apple", "Banana", "Orange"];
  
  return (
    <ul>
      {items.map((item, index) => <li key={index}>{item}</li>)}
    </ul>
  );
}

export default List;
```

---

## 10. **Component Lifecycle**

Lifecycle methods are used in class components to run code at different stages of a component’s existence.

### Common Lifecycle Methods:
- `componentDidMount()`: Called after the component is mounted.
- `componentDidUpdate()`: Called after the component updates.
- `componentWillUnmount()`: Called before the component is removed from the DOM.

```jsx
import React, { Component } from 'react';

class LifecycleDemo extends Component {
  componentDidMount() {
    console.log("Component mounted!");
  }

  componentWillUnmount() {
    console.log("Component will unmount!");
  }

  render() {
    return <h1>Lifecycle Methods in React</h1>;
  }
}

export default LifecycleDemo;
```

---

## 11. **Hooks in React**

React Hooks are functions that allow you to use state and other React features in functional components. The most common hooks are `useState`, `useEffect`, and `useContext`.

### useState Hook
The `useState` hook lets you add state to functional components.

```jsx
import React, { useState } from 'react';

const Toggle = () => {
  const [isOn, setIsOn] = useState(false);

  return (
    <button onClick={() => setIsOn(!isOn)}>
      {isOn ? 'ON' : 'OFF'}
    </button>
  );
}

export default Toggle;
```

### useEffect Hook
The `useEffect` hook is used for side effects like fetching data, manually changing the DOM, etc.

```jsx
import React, { useState, useEffect } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []);  // Empty array means this effect runs once, when the component mounts

  if (!data) {
    return <div>Loading...</div>;
  }

  return <div>{data.name}</div>;
}

export default DataFetcher;
```

---

## 12. **Context API**

The Context API allows you to share data across components without explicitly passing props at every level.

```jsx
import React, { useState, createContext, useContext } from 'react';

// Create Context
const MyContext = createContext();

// Provider component
const MyProvider = ({ children }) => {
  const [state, setState] = useState("Hello from Context");

  return (
    <MyContext.Provider value={{ state, setState }}>
      {children}
    </MyContext.Provider>
  );
};

// Consumer component
const MyComponent = () => {
  const { state } = useContext(MyContext);
  return <div>{state}</div>;
}

const App = () => {
  return (
    <MyProvider>
      <MyComponent />
    </MyProvider>
  );
}

export default App;
```

---

## 13. **React Router**

React Router is a standard library for routing in React, allowing you to create single-page applications with navigation.

```bash
npm install react-router-dom
```

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

const Home = () => <h1>Home Page</h1>;
const About = () => <h1>About Page</h1>;

const App = () => {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Route path="/" exact component={Home} />
      <Route path="/about" component={About} />
    </Router>
  );
}

export default App;
```

---

### Conclusion:
React is a powerful and flexible library for building modern user interfaces. By utilizing its core concepts—components, props, state, hooks, and lifecycle methods—you can create dynamic and performant web applications. React's component-based architecture, along with the virtual DOM, provides excellent performance and makes building complex UIs more manageable.
