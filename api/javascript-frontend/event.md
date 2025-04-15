## Event

This can invoke events from Python to JavaScript.

### Python Backend

In Python, you can use specific libraries to trigger events. For example, you can use the `pyloid` library to trigger events.

```python
# Invoke the 'hello_event' event with a message
window.invoke('hello_event', {'message': 'Hello from Python!'})
```

### JavaScript Frontend

In JavaScript, you can receive and handle events triggered from Python. You can use the `pyloid-js` library to receive events.

```javascript
import { event } from 'pyloid-js';

// Register the event listener
event.listen('hello_event', (data) => {
    console.log('hello_event', data.message);
});

// Unregister the event listener
event.unlisten('hello_event');
```