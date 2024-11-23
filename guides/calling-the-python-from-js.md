# Calling Python from JS

## Introduction to PylonAPI

The `PyloidAPI` class is a core component that enables interaction between JavaScript and Python.

### PyloidAPI Properties

The PyloidAPI class has the following important properties:

- `window`: References the BrowserWindow instance.
- `app`: References the Pyloid application instance.
- `window_id`: Unique identifier for the browser window.

## Using the Bridge Decorator

The `PyloidAPI` class is used with the `Bridge` decorator to make Python methods callable from JavaScript.

### Bridge Decorator Parameters

The `Bridge` decorator can use the following parameters:

- `result`: Specifies the return type.
- `args`: Specifies the argument types.

## Setting up JavaScript API in Python

{% tabs %}
{% tab title="main.py" %}

```python
from pyloid import Pyloid, PyloidAPI, Bridge

app = Pyloid("Pyloid-App")

class CustomAPI(PyloidAPI):
    @Bridge(str, result=str)
    def echo(self, message):
        return f"Message received in Python: {message}"

# Create main window
window = app.create_window(
    title="Pyloid Browser",
    js_apis=[CustomAPI()],
)

window.load_file("index.html")

window.show()
window.focus()

app.run()
```

{% endtab %}

{% tab title="index.html" %}

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pyloid</title>
    <script>
      document.addEventListener('pyloidReady', async function () {
        console.log('Pyloid is ready');

        let result = await window.pyloid.CustomAPI.echo('Hello, Pyloid!');
        document.querySelector('p').textContent = result;
      });
    </script>
  </head>
  <body>
    <h1>Hello!</h1>
    <p>None</p>
  </body>
</html>
```

{% endtab %}
{% endtabs %}
