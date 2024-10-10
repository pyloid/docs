# Calling the Python from JS

## Introduction to PylonAPI

The `PyloidAPI` class is a key component that enables interaction between JavaScript and Python.

## Using the Bridge Decorator

The `PyloidAPI` class is used in conjunction with the `Bridge` decorator to allow Python methods to be called from JavaScript.

### Bridge Decorator Parameters

The `Bridge` decorator can use the following parameters:

- `result`: Specifies the return type.
- `args`: Specifies the argument types.

## Setting up JavaScript API in Python

Here's an example code using `PylonAPI` and the `Bridge` decorator:

```python
from pyloid import PyloidAPI, Bridge

class CustomAPI(PyloidAPI):
    @Bridge(str, int, result=str)
    def echo(self, message, number):
        print(f"Message: {message}-{number}")
        return f"Message received in Python: {message}-{number}"

    @Bridge(result=str)
    def getAppVersion(self):
        return "1.0.0"

    @Bridge(result=str)
    def create_window(self):
        window = app.create_window(
            title="Pyloid Browser2",
            frame=True,
            context_menu=False,
        )

        window.set_size(800, 600)
        window.set_position(0, 0)
        window.load_url("https://www.google.com")
        window.show()
        window.focus()

        return window.id

# Create main window
window = app.create_window(
    title="Pyloid Browser1",
    frame=True,
    js_apis=[CustomAPI()],
    dev_tools=True
)

if (is_production()):
    window.load_file(os.path.join(get_production_path() + "/index.html"))
else:
    window.load_file("index.html")

window.show()
window.focus()

app.run()
```

### Code Explanation

1. The `CustomAPI` class is defined by inheriting from `PyloidAPI`.

2. `echo` method:

   - Uses the `Bridge` decorator to make it callable from JavaScript.
   - Takes a string and an integer as arguments, and returns a string.

3. `getAppVersion` method:

   - Returns the application version.

4. `create_window` method:

   - Creates a new window, configures it, and returns the window ID.

5. Main window creation:
   - Passes an instance of `CustomAPI` as the `js_apis` parameter to allow access to Python methods from JavaScript.

This example demonstrates how to call Python methods from JavaScript and how to use `PyloidAPI` to create and manage windows.

## Calling Python Methods from JavaScript

Here's how to call Python methods defined in JavaScript:

```javascript
// CustomAPI method usage examples

// Using the echo method
pyloid.CustomAPI.echo('Hello', 42).then((result) => {
  console.log(result); // Outputs "Message received in Python: Hello-42"
});

// Using the getAppVersion method
document.addEventListener('pyloidReady', function () {
  pyloid.CustomAPI.getAppVersion().then((version) => {
    console.log('App version:', version); // Outputs "App version: 1.0.0"
  });

  // Example using async/await syntax
  async function useCustomAPI() {
    try {
      const echoResult = await pyloid.CustomAPI.echo('Test', 100);
      console.log(echoResult);

      const appVersion = await pyloid.CustomAPI.getAppVersion();
      console.log('Current app version:', appVersion);
    } catch (error) {
      console.error('Error occurred while calling API:', error);
    }
  }

  useCustomAPI();

  // Binding button click event
  document.getElementById('myButton').addEventListener('click', function () {
    // Using the create_window method
    pyloid.CustomAPI.create_window().then((windowId) => {
      console.log('New window ID:', windowId); // Outputs "New window ID: [created window ID]"
    });
  });
});
```

### Code Explanation

1. `pyloidReady` event:

   - Uses `document.addEventListener('pyloidReady', function () {...})` to define code to be executed when Pyloid is ready.
   - Python methods can be called within this event handler.
   - **Boilerplates like React execute JavaScript itself after `pyloidReady`, so there's no need to add a separate `pyloidReady` event listener. Therefore, when using a boilerplate, you can call Python methods directly.**

2. Calling the `echo` method:

   - Uses `pyloid.CustomAPI.echo()` to call the `echo` method in Python.
   - The result is returned as a Promise and handled using `then()`.

3. Calling the `getAppVersion` method:

   - Calls `pyloid.CustomAPI.getAppVersion()` to get the app version.

4. Using async/await:

   - The `useCustomAPI` function uses async/await syntax to handle asynchronous calls more simply.

5. Button click event:

   - Calls the `create_window` method to create a new window when the button is clicked.
