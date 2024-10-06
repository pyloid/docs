# PylonAPI

The `PylonAPI` class is implemented by inheriting from QObject.

## Used with Bridge

The `PylonAPI` class is used in conjunction with the `Bridge` decorator to enable interaction between JavaScript and Python. The `Bridge` decorator allows Python methods to be called from JavaScript.

### `Bridge` Decorator

The `Bridge` decorator can take the following parameters:
- `result`: Specifies the return type.
- `args`: Specifies the argument types.

## Usage Example
```python
from PylonAPI import PylonAPI, Bridge

class CustomAPI(PylonAPI):
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
            title="Pylon Browser2",
            frame=True,
            context_menu=False,
            js_apis=[CustomAPI()],
            dev_tools=True
        )

        window.set_size(800, 600)
        window.set_position(0, 0)
        window.load_url("https://www.google.com")
        window.show()
        window.focus()

        return window.id
```