# Calling Python Functions from JavaScript

Pyloid is a Python-based desktop app framework that allows easy function calls between frontend (JavaScript) and backend (Python) via a Remote Procedure Call (RPC) system. This document explains how to call Python functions from JavaScript using Pyloid's RPC system.

## 1. Defining RPC Functions in Python

All RPC functions must be defined as asynchronous (async) functions and registered with the `@rpc.method()` decorator. Additionally, if you add `ctx` (context) as the first argument, you can access the current app and window objects.

```python
from pyloid.rpc import PyloidRPC, RPCContext

rpc = PyloidRPC()

@rpc.method()
async def greet(name: str):
    return f"Hello, {name}!"

@rpc.method()
async def set_title(ctx: RPCContext, title: str):
    ctx.window.set_title(title)
    return "Title changed!"
```

In the example above, the `greet` function simply returns a greeting, and the `set_title` function changes the title of the current window. You can access the current window (`ctx.window`) through `ctx`.

## 2. Calling RPC Functions from JavaScript

On the frontend, you can use Pyloid's `rpc.call` method to call Python RPC functions. Just pass the function name and arguments.

```javascript
import { rpc } from 'pyloid-js';

rpc.call('greet', { name: 'World' })
    .then(response => {
        console.log(response); // "Hello, World!"
    })
    .catch(error => {
        console.error('RPC call failed:', error);
    });

rpc.call('set_title', { title: 'New Window Title' })
    .then(response => {
        console.log(response); // "Title changed!"
    });
```

## 3. Notes

- All RPC functions must be defined as async and can freely use await internally.
- If you add ctx (RPCContext) as a function argument, you can access the app and window objects.
- You can call the function immediately from the frontend by just passing the function name and arguments.
- All GUI-related functions in Pyloid are designed to be thread-safe, so you can safely call them even if you're not on the main thread.