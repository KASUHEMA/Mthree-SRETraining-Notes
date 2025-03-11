# DOM and Node.js

## What is the DOM?

The **Document Object Model (DOM)** is a programming interface for web documents. It represents the structure of a document as a tree of objects, where each object corresponds to a part of the document, such as elements, attributes, and text nodes.

### Key Features of the DOM:
- Allows dynamic changes to the document structure, style, and content.
- Represents the document as a tree of nodes.
- Enables interaction with the document using JavaScript.
- Used primarily in web browsers.

### Example of DOM Manipulation (JavaScript in Browser):
```javascript
// Changing the text of a paragraph with id "demo"
document.getElementById("demo").innerText = "Hello, DOM!";
```

## What is Node.js?

**Node.js** is a runtime environment that allows JavaScript to be executed outside the browser. It is built on the V8 JavaScript engine and provides various built-in modules to interact with the operating system, file system, and network.

### Key Features of Node.js:
- Asynchronous and event-driven.
- Uses a non-blocking I/O model for high scalability.
- Supports JavaScript execution outside the browser.
- Has a rich ecosystem of npm (Node Package Manager) modules.

### Example of a Simple Node.js Server:
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, Node.js!');
});

server.listen(3000, () => {
    console.log('Server running at http://localhost:3000/');
});
```

## Differences Between DOM and Node.js

| Feature      | DOM | Node.js |
|-------------|-----|---------|
| Environment | Browser | Server-side |
| API | Manipulates HTML & CSS | Handles OS, File System, and HTTP requests |
| Event Model | Uses event listeners on elements | Uses event-driven programming |
| Execution | Runs in browser | Runs outside the browser |

## Conclusion

The DOM is essential for interacting with web pages in the browser, while Node.js enables JavaScript to run on the server. While they both use JavaScript, they serve different purposes and provide different functionalities.

# React Project Documentation

## Overview
This project is a React application with multiple components, including a counter, a to-do list, a theme switcher, and a table. It utilizes React Router for navigation and includes styling through CSS.

---

## Project Setup
### Install Dependencies
Ensure you have **Node.js** installed. Then run:
```sh
npm install
```

### Start the Application
```sh
npm start
```
This will start the development server at `http://localhost:3000`.

---

## File Structure
```
📂 src/
├── 📜 App.js
├── 📜 Counter.js
├── 📜 Table.js
├── 📜 ThemeSwitcher.js
├── 📜 Todo.js
├── 📜 index.js
├── 📜 styles.css
├── 📜 App.css
├── 📜 index.css
```

---

## Components

### **1. App.js** (Main Router & Navigation)
This file is responsible for routing and navigation. It uses **React Router** to switch between different components dynamically.
```jsx
import { Routes, Route, Link, useLocation, useNavigate } from 'react-router-dom';
import Counter from './Counter';
import Todo from './Todo';
import ThemeSwitcher from './ThemeSwitcher';
import Table from './Table';
import './styles.css';

function App() {
    const location = useLocation(); // Get the current route
    const navigate = useNavigate(); // Used for navigation

    const showMenu = location.pathname === "/"; // Show menu only on the home page
    const showExitButton = !showMenu; // Show exit button when a component is selected

    return (
        <div className="app-container">
            {showMenu && (
                <nav>
                    <Link to="/counter">Counter</Link>
                    <Link to="/todo">Todo</Link>
                    <Link to="/themeswitcher">Theme Switcher</Link>
                    <Link to="/table">Table</Link>
                </nav>
            )}

            {showExitButton && (
                <button className="exit-button" onClick={() => navigate("/")}>Exit</button>
            )}

            <Routes>
                <Route path="/" element={<div className="empty-content">Select an option from the menu</div>} />
                <Route path="/counter" element={<Counter />} />
                <Route path="/todo" element={<Todo />} />
                <Route path="/themeswitcher" element={<ThemeSwitcher />} />
                <Route path="/table" element={<Table />} />
            </Routes>
        </div>
    );
}

export default App;
```
![image](https://github.com/user-attachments/assets/017497ea-6121-4856-b447-9af91d00e369)


### **2. Counter.js** (A Simple Counter)
This component maintains a **count state** and provides buttons to **increment, decrement, and reset** the count.
```jsx
import React, { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div className="container">
            <h2>Counter: {count}</h2>
            <button className="btn-primary" onClick={() => setCount(count + 1)}>Increment</button>
            <button className="btn-danger" onClick={() => setCount(count - 1)}>Decrement</button>
            <button className="btn-reset" onClick={() => setCount(0)}>Reset</button>
        </div>
    );
}

export default Counter;
```
![image](https://github.com/user-attachments/assets/d362be01-2b09-41ab-a69b-909661507b06)

### **3. Todo.js** (A Simple To-Do List)
This component allows users to add tasks to a **to-do list**. The tasks are stored in a state variable and displayed as a list.
```jsx
import React, { useState } from 'react';

function Todo() {
    const [task, setTask] = useState('');
    const [todos, setTodos] = useState([]);

    const addTodo = () => {
        if (task.trim() && !todos.some(todo => todo.text === task.trim())) {
            setTodos([...todos, { id: Date.now(), text: task.trim(), completed: false }]);
            setTask('');
        }
    };

    const deleteTodo = (id) => {
        setTodos(todos.filter(todo => todo.id !== id));
    };

    const toggleComplete = (id) => {
        setTodos(todos.map(todo => todo.id === id ? { ...todo, completed: !todo.completed } : todo));
    };

    return (
        <div className="container">
            <h2>Todo List</h2>
            <input 
                type="text" 
                value={task} 
                onChange={(e) => setTask(e.target.value)} 
                placeholder="Add a task" 
            />
            <button className="btn-primary" onClick={addTodo}>Add Task</button>
            <ul>
                {todos.map((todo) => (
                    <li key={todo.id} style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}>
                        <span onClick={() => toggleComplete(todo.id)}>{todo.text}</span>
                        <button className="btn-delete" onClick={() => deleteTodo(todo.id)}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );
}

export default Todo;

```
![image](https://github.com/user-attachments/assets/628aa415-cbdb-4fd1-af4c-d58cc3ce4755)

### **4. ThemeSwitcher.js** (Light/Dark Mode Toggle)
This component toggles between **light mode** and **dark mode** using a state variable.
```jsx
import React, { useState } from 'react';

function ThemeSwitcher() {
    const [darkMode, setDarkMode] = useState(false);

    return (
        <div className="container" style={{ backgroundColor: darkMode ? '#333' : '#fff', color: darkMode ? '#fff' : '#000' }}>
            <h2>Theme Switcher</h2>
            <button className="btn-primary" onClick={() => setDarkMode(!darkMode)}>
                {darkMode ? 'Light Mode' : 'Dark Mode'}
            </button>
        </div>
    );
}

export default ThemeSwitcher;
```
![image](https://github.com/user-attachments/assets/d5fc9b16-a52f-45f8-a691-a7dfb38c1294)

### **5. Table.js** (Dynamic Table Input)
This component allows users to **add rows dynamically** to a table.
```jsx
import React, { useState } from 'react';

function Table() {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [age, setAge] = useState('');
    const [rows, setRows] = useState([]);

    const submit = () => {
        if (name.trim() && email.trim() && age.trim()) {
            setRows([...rows, { name, email, age }]);
            setName('');
            setEmail('');
            setAge('');
        } else {
            alert("Please fill in all fields before submitting.");
        }
    };

    return (
        <div className="container">
            <h2>Table</h2>
            <input type="text" value={name} onChange={(e) => setName(e.target.value)} placeholder="Name" />
            <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} placeholder="Email" />
            <input type="number" value={age} onChange={(e) => setAge(e.target.value)} placeholder="Age" />
            <button className="btn-primary" onClick={submit}>Submit</button>

            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Age</th>
                    </tr>
                </thead>
                <tbody>
                    {rows.map((row, index) => (
                        <tr key={index}>
                            <td>{row.name}</td>
                            <td>{row.email}</td>
                            <td>{row.age}</td>
                        </tr>
                    ))}
                </tbody>
            </table>
        </div>
    );
}

export default Table;
```
![image](https://github.com/user-attachments/assets/db6f0793-5a14-41df-a819-a56c5880b0e2)

---

## Conclusion
This React project covers routing, state management, and styling, creating an interactive and user-friendly application. 

