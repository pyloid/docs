# PyloidRPC

Pyloid is a Python-based desktop app framework that allows easy function calls between the frontend (web) and backend (Python) through an RPC (Remote Procedure Call) system.  
Below is a guide on how to use Pyloid's RPC system, along with various examples of utilizing app/window objects within RPC functions.

## Basic Usage

Here's how to set up and use the RPC system:

```python
from pyloid.rpc import PyloidRPC, RPCContext

# Create an RPC instance
rpc = PyloidRPC()

# Register a simple RPC method
@rpc.method()
async def greet(name: str):
    return f"Hello, {name}!"

# Register a method that uses context
@rpc.method()
async def create_google_window(ctx: RPCContext):
    window = ctx.pyloid.create_window(title="Google")
    window.load_url("https://www.google.com")
    window.show_and_focus()
```

## Context Injection

Pyloid RPC automatically injects a `RPCContext` object when a parameter named `ctx` is present in your method signature. This context provides access to:

- `ctx.pyloid`: The Pyloid application instance
- `ctx.window`: The current browser window instance

This makes it easy to interact with the application state from your RPC methods.

## RPC Method Decorator

```python
@rpc.method(name: Optional[str] = None)
```

### Parameters

- `name` (str, optional): Custom name for the RPC method. If not provided, the function name will be used.

### Requirements

- The decorated function must be an async function
- Function parameters can be typed and will be properly passed from JSON-RPC calls
- Including a `ctx` parameter will automatically inject the context object

## RPCContext Object

The `RPCContext` class provides access to the current application state:

### Example with Context

```python
@rpc.method()
async def toggle_fullscreen(ctx: RPCContext):
    # Access the current window through context
    is_fullscreen = ctx.window.is_fullscreen()
    ctx.window.set_fullscreen(not is_fullscreen)
    return not is_fullscreen
```

## Advanced Error Handling

Pyloid provides a custom `RPCError` class for handling application-specific errors:

```python
@rpc.method()
async def divide(a: float, b: float):
    if b == 0:
        # Create a custom error with code and message
        raise RPCError("Division by zero is not allowed", code=-32000)
    return a / b
```

## Starting the RPC Server

Pyloid's RPC system does not require a separate server. Instead, you can connect the RPC instance to the window when creating it. When creating a window, pass the RPC instance to the `rpc` parameter, and the window will automatically enable RPC functionality.

```python
# Create an RPC instance
rpc = PyloidRPC()

# Connect the RPC instance when creating a window
window = app.create_window(
    title="My App Window",
    rpc=rpc  # Connect the RPC instance to the window
)
```

This method is particularly useful in Pyloid's multi-window environment. You can connect different RPC instances to each window or share a single RPC instance across multiple windows. When an RPC request is processed through a window, it can access the window and the application instance through the context (`ctx`).

The RPC server also uses dynamic port allocation internally, so it will always start with an available port without port conflicts.

## Calling RPC Methods from Frontend

Once your RPC server is running, you can call your methods from the frontend:

```javascript
const result = await window.pyloid.rpc.call('greet', ['World']);
console.log(result);  // Outputs: "Hello, World!"

await window.pyloid.rpc.call('create_window');
```

## Complete Example

Here's a complete example that shows how to set up an RPC server with the static file server:

```python
from pyloid import Pyloid
from pyloid.rpc import PyloidRPC, RPCContext
from pyloid.serve import pyloid_serve

# Initialize RPC
rpc = PyloidRPC()

@rpc.method()
async def get_window_info(ctx: RPCContext):
    return {
        "id": ctx.window.get_id(),
        "window_title": ctx.window.get_title(),
        "size": ctx.window.get_size(),
        "position": ctx.window.get_position(),
        "url": ctx.window.get_url(),
        "is_fullscreen": ctx.window.is_fullscreen(),
        #...
    }

# Initialize Pyloid
app = Pyloid("My Pyloid App")

if is_production():
    url = pyloid_serve("dist-front")
else:
    url = "http://localhost:5173"

# Create window with RPC enabled
window = app.create_window(
    title="My App Window",
    rpc=rpc  # Pass the RPC instance to enable it for this window
)

# Load the frontend
window.load_url(url)
window.show_and_focus()

# Start the application (this will start the event loop)
app.run()
```
---

## Notes

- All RPC functions must be defined as async, and you can freely use await inside them.
- When calling RPC functions from the frontend, simply pass the function name and parameters as they are.
- Complex GUI control and app state management can also be easily implemented via RPC.
- **All GUI-related functions in Pyloid are designed to be thread-safe.**  
  Therefore, unlike typical Python GUI frameworks, you can safely call GUI-related methods (app, window, etc.) inside RPC functions (asynchronous/other threads) even if they are not on the main thread.  
  Without any additional synchronization or queuing, you can freely control the GUI from RPC.
