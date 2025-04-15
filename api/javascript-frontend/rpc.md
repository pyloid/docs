## RPC

```javascript
import { rpc } from 'pyloid-js';

// Call the 'greet' RPC function to receive a greeting.
rpc.call('greet', {name: 'Alice'})
  .then(response => {
    console.log(response); // Outputs "Hello, Alice!"
  })
  .catch(error => {
    console.error("Error occurred during RPC call:", error);
  });
```

This example demonstrates how to call the `greet` RPC function from the frontend, passing a name and receiving a greeting message. The `rpc.call` method is used to pass the function name and required parameters. If the call is successful, the response message is printed to the console, and if an error occurs, the error message is printed.

```python
@rpc.method()
async def greet(name: str):
    return f"Hello, {name}!"
```

This is an example of the `greet` RPC function defined in Python. This function takes a name and returns a greeting message. You can call this function from the frontend to receive a greeting message.
