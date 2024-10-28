# Loading Webview

### `load_url` (Loading URL)

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Pyloid-Window")

window.load_url("https://www.example.com")

window.show()
```

### `load_file` (Loading File)

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Pyloid-Window")

window.load_file("./index.html")

window.show()
```

### `load_html` (Loading HTML)

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Pyloid-Window")

window.load_html("<h1>Hello, Pyloid!</h1>")

window.show()
```
