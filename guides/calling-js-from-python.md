# Calling JavaScript from Python

Pyloid provides a mechanism for calling JavaScript functions from Python through events. This guide explains how to invoke JavaScript event handlers from Python backend code.

## 1. Event System Overview

The event system in Pyloid allows the Python backend to trigger events that can be captured and handled by the JavaScript frontend. This creates a communication channel from the backend to the frontend.

## 2. Invoking Events from Python

In the Python backend, you can use the `invoke()` method to trigger events that will be received by the JavaScript frontend:

```python
app = Pyloid(app_name="Pyloid-App")
window = app.create_window("pyloid-window")

# Invoke an event named 'hello_event' with data
window.invoke('hello_event', {'message': 'Hello from Python!'})
```

The first parameter is the event name that JavaScript will listen for, and the second parameter is the data payload to send with the event. The data can be any JSON-serializable object.

## 3. Handling Events in JavaScript

In the JavaScript frontend, you need to set up event listeners to capture and respond to events triggered from Python:

```javascript
import { event } from 'pyloid-js';

// Register an event listener for 'hello_event'
event.listen('hello_event', (data) => {
    console.log('Received hello_event with message:', data.message);
    // Handle the event data here
});
```

## 4. Removing Event Listeners

When you no longer need an event listener, you should clean it up to prevent memory leaks:

```javascript
import { event } from 'pyloid-js';

// Unregister the event listener
event.unlisten('hello_event');
```

## 5. Use Cases

The event system is useful for various scenarios:
- Notifying the frontend of backend state changes
- Sending real-time updates from long-running Python processes
- Pushing notifications from the backend to the user interface
- Coordinating UI updates based on backend processing results

## 6. Important Notes

- Events are one-way communications from Python to JavaScript
- For two-way communication, combine events with RPC calls
- Event names should be consistent between Python and JavaScript
- The data payload should be kept reasonably small for best performance
