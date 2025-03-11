# React Basics

## Introduction to React
React is a JavaScript library for building user interfaces. It is used to create single-page applications (SPA) with a component-based architecture.

### Features of React
- **Component-Based**: UI is broken down into reusable components.
- **Virtual DOM**: Optimizes rendering performance.
- **Declarative UI**: Updates the UI based on state changes.
- **Unidirectional Data Flow**: Data flows in one direction, making debugging easier.
- **Hooks**: Use state and lifecycle features without writing a class.

---

## Installation & Setup
To start using React, first install Node.js and create a React project using create-react-app:

```sh
npx create-react-app my-app
cd my-app
npm start
```

This sets up a development environment with Webpack, Babel, and React.

---

## JSX (JavaScript XML)
JSX is a syntax extension for JavaScript that looks like HTML but allows JavaScript expressions.

```jsx
function Greeting() {
    return <h1>Hello, World!</h1>;
}
```

---

## Components
React components can be **functional** or **class-based**.

### Functional Component
```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}!</h1>;
}
```

### Class Component
```jsx
class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}!</h1>;
    }
}
```

---

## State & Props
### **Props (Properties)**
Props are used to pass data between components.
```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}!</h1>;
}
```

### **State**
State is used to manage data inside a component.
```jsx
import { useState } from 'react';
function Counter() {
    const [count, setCount] = useState(0);
    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
    );
}
```

---

## Handling Events
React uses camelCase for event names.
```jsx
function Button() {
    function handleClick() {
        alert('Button Clicked!');
    }
    return <button onClick={handleClick}>Click Me</button>;
}
```

---

## Conditional Rendering
Render components conditionally using `if`, `&&`, or the ternary `?` operator.
```jsx
function Greeting(props) {
    return props.isLoggedIn ? <h1>Welcome Back!</h1> : <h1>Please Sign In</h1>;
}
```

---

## Lists & Keys
Rendering lists in React.
```jsx
const names = ['Alice', 'Bob', 'Charlie'];
function NameList() {
    return (
        <ul>
            {names.map((name, index) => <li key={index}>{name}</li>)}
        </ul>
    );
}
```

---

## Forms in React
Handling form inputs using state.
```jsx
function Form() {
    const [input, setInput] = useState('');
    return (
        <form>
            <input value={input} onChange={(e) => setInput(e.target.value)} />
            <p>You typed: {input}</p>
        </form>
    );
}
```

---

## React Router
To enable navigation in React apps.
```sh
npm install react-router-dom
```

```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function Home() { return <h1>Home Page</h1>; }
function About() { return <h1>About Page</h1>; }

function App() {
    return (
        <BrowserRouter>
            <nav>
                <Link to='/'>Home</Link>
                <Link to='/about'>About</Link>
            </nav>
            <Routes>
                <Route path='/' element={<Home />} />
                <Route path='/about' element={<About />} />
            </Routes>
        </BrowserRouter>
    );
}
```

---

## React Hooks
### **useState Hook**
Manages state in functional components.
```jsx
const [count, setCount] = useState(0);
```

### **useEffect Hook**
Runs side effects in a component.
```jsx
useEffect(() => {
    console.log('Component mounted');
}, []);
```

### **useContext Hook**
Manages global state without prop drilling.
```jsx
const ThemeContext = React.createContext('light');
const theme = useContext(ThemeContext);
```

---

## Fetching Data with useEffect
```jsx
import { useEffect, useState } from 'react';
function DataFetching() {
    const [data, setData] = useState([]);
    useEffect(() => {
        fetch('https://jsonplaceholder.typicode.com/posts')
            .then(response => response.json())
            .then(data => setData(data));
    }, []);
    return (
        <ul>
            {data.map(post => <li key={post.id}>{post.title}</li>)}
        </ul>
    );
}
```

---

## Conclusion
React is a powerful library that makes building UI components easy and efficient. By mastering components, state, hooks, and routing, you can create dynamic and scalable applications.



