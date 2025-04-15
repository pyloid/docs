# Calling Python from JavaScript

Pyloid is a Python-based desktop app framework that enables easy function calls between the frontend (JavaScript) and backend (Python) through a Remote Procedure Call (RPC) system. This document explains how to call Python functions from JavaScript using Pyloid's RPC system.

## 1. Defining RPC Functions in Python

First, you need to define RPC functions in the Python backend. All RPC functions must be defined as asynchronous functions and registered as RPC functions using the `@rpc.method()` decorator.

```python
from pyloid import app, rpc

@rpc.method()
async def greet(name: str):
    return f"Hello, {name}!"
```

In the example above, we defined a simple RPC function called `greet`. This function takes a name as an argument and returns a greeting message.

## 2. Calling RPC Functions from JavaScript

In the frontend, you can call Python RPC functions using Pyloid's `rpc.call` method. You call it by passing the function name and arguments.

```javascript
import { rpc } from 'pyloid-js';

rpc.call('greet', { name: 'World' })
    .then(response => {
        console.log(response); // "Hello, World!"
    })
    .catch(error => {
        console.error('RPC call failed:', error);
    });
```

In the JavaScript code above, we call the `greet` function and output the returned message to the console.

## 3. Important Notes

- All RPC functions must be defined as asynchronous functions, and you can freely use `await` within them.
- When calling RPC functions from the frontend, you just need to pass the function name and arguments directly.
- All of Pyloid's GUI-related functions are designed to be thread-safe, so they can be safely called from outside the main thread.