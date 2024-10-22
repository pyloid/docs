# Customizing API using PySide

Pyloid is built on PySide6 and provides functionality for users to extend the API directly. This allows easy use of various PySide6 features in Pyloid applications.

## How to Create Custom APIs

1. Inherit from the `PyloidAPI` class to create a new class.
2. Define desired methods and use the `@Bridge` decorator to connect with JavaScript.
3. Utilize PySide6 features within the methods.

## Examples

### Implementing File Open Dialog

```python
from PySide6.QtWidgets import QFileDialog
from pyloid import PyloidAPI, Bridge

class CustomAPI(PyloidAPI):
    @Bridge(result=str)
    def open_file(self):
        file, _ = QFileDialog.getOpenFileName(filter="Text files (*.txt)")
        return file if file else ""

    @Bridge(result=str)
    def save_file(self):
        file, _ = QFileDialog.getSaveFileName(filter="Text files (*.txt)")
        return file if file else ""

    @Bridge(result=str)
    def select_directory(self):
        directory = QFileDialog.getExistingDirectory()
        return directory if directory else ""
```

### Implementing Message Box

```python
from PySide6.QtWidgets import QMessageBox
from pyloid import PyloidAPI, Bridge

class MessageAPI(PyloidAPI):
    @Bridge(str, str, result=str)
    def show_info(self, title: str, message: str):
        QMessageBox.information(None, title, message)

    @Bridge(str, str,result=str)
    def show_warning(self, title: str, message: str):
        QMessageBox.warning(None, title, message)

    @Bridge(str, str,result=bool)
    def show_question(self, title: str, message: str):
        reply = QMessageBox.question(None, title, message)
        return reply == QMessageBox.Yes
```

## How to Use

1. Define custom API classes.
2. Pass API instances when creating a Pyloid application.

```python
from pyloid import Pyloid

app = Pyloid(app_name="CustomApp")

window = app.create_window(title="Custom API Example", js_apis=[CustomAPI(), MessageAPI()])
window.load_file("path/index.html")
window.show()

app.run()
```

3. Using the API in HTML/JavaScript:

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="qrc:///qtwebchannel/qwebchannel.js"></script>
  </head>
  <body>
    <button id="openFile">Open File</button>
    <button id="showMessage">Show Message</button>

    <script>
      document.addEventListener('pyloidReady', function () {
        async function openFile() {
          const filePath = await window.pyloid.CustomAPI.open_file();
          console.log('Selected file:', filePath);
        }

        async function showMessage() {
          await window.pyloid.MessageAPI.show_info(
            'Information',
            'This is a custom API test.'
          );
        }

        document.querySelector('#openFile').addEventListener('click', openFile);
        document
          .querySelector('#showMessage')
          .addEventListener('click', showMessage);
      });
    </script>
  </body>
</html>
```

## Precautions

1. When using the `@Bridge` decorator, you must specify the types of input parameters and return values. For example:
   - No input parameters and returns a string: `@Bridge(result=str)`
   - Takes two strings as input and returns a boolean: `@Bridge(str, str, result=bool)`
   - Takes an integer as input and returns a string: `@Bridge(int, result=str)`
2. When returning complex objects, they must be converted to a JSON-serializable form.
3. UI-related tasks should be executed on the main thread.

In this way, you can integrate various PySide6 features into Pyloid applications. More complex features like `QtSql`, `QtBluetooth`, `QtMultimedia`, `QtNetwork`, etc., can also be implemented as needed.
