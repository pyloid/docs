# PyloidRPC

Pyloid is a Python-based desktop app framework that allows easy function calls between the frontend (web) and backend (Python) through an RPC (Remote Procedure Call) system.  
Below is a guide on how to use Pyloid's RPC system, along with various examples of utilizing app/window objects within RPC functions.

---

## 1. Using App/Window Objects in RPC Functions

Within Pyloid's RPC functions, you can freely use various GUI-related objects and methods such as app and window.  
Here are some representative usage examples.

### 1-1. Change Window Size

```python
@rpc.method()
async def resize_window(width: int, height: int):
    window.set_size(width, height)
    return f"Window size changed to {width}x{height}."
```

### 1-2. Set App Auto Start

```python
@rpc.method()
async def set_auto_start(enable: bool):
    app.set_auto_start(enable)
    return f"Auto start has been {'enabled' if enable else 'disabled'}."
```

---

## 2. Calling RPC Functions from the Frontend

On the frontend (e.g., JavaScript), you can call Pyloid's RPC functions as shown below.

```javascript
import { rpc } from 'pyloid-js';

rpc.call('resize_window', {width: 800, height: 600})
```

---

## 3. Advanced Example: File Saving and State Management

By combining Pyloid's store feature with RPC, you can also save and load app state.

```python
store = app.store("store.json")

@rpc.method()
async def save_value(key: str, value):
    store.set(key, value)
    store.save()
    return "Save complete"

@rpc.method()
async def get_value(key: str):
    return store.get(key)
```

---

## 4. Other Usage Examples

### 4-1. Multi-Window Control

```python
@rpc.method()
async def open_new_window():
    new_win = app.create_window("New Window")
    new_win.load_file("file/another.html")
    new_win.show_and_focus()
    return "New window opened"
```

---

## 5. Notes

- All RPC functions must be defined as async, and you can freely use await inside them.
- When calling RPC functions from the frontend, simply pass the function name and parameters as they are.
- Complex GUI control and app state management can also be easily implemented via RPC.
- **All GUI-related functions in Pyloid are designed to be thread-safe.**  
  Therefore, unlike typical Python GUI frameworks, you can safely call GUI-related methods (app, window, etc.) inside RPC functions (asynchronous/other threads) even if they are not on the main thread.  
  Without any additional synchronization or queuing, you can freely control the GUI from RPC.
