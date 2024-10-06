# Utility Functions

## `get_production_path()`

Returns the path for resource files in the production environment.

### Parameters

None

### Return Value

- `Optional[str]`: The path of resource files in the production environment. Returns `None` if running as a regular Python script.

### Description

This function checks if the current execution environment is a production environment (e.g., an executable built with PyInstaller) and returns the path of resource files if it is. If running as a regular Python script, it returns `None`.

## `is_production()`

Checks if the current environment is a production environment.

### Parameters

None

### Return Value

- `bool`: Returns `True` if it's a production environment, `False` otherwise.

### Description

This function checks if the current execution environment is a production environment (e.g., an executable built with PyInstaller). It examines the `sys.frozen` attribute to determine if it's a production environment.

## Usage Example

### Example 1

```python
app = PylonApp(single_instance=True)

if (is_production()):
    app.set_icon(os.path.join(get_production_path() + "/icon.ico"))
else:
    app.set_icon("assets/icon.ico")
    app.set_tray_icon("assets/icon.ico")
```

### Example 2

```python
if (is_production()):
    window.load_file(os.path.join(get_production_path() + "/file/index.html"))
else:
    window.load_url("http://localhost:5173")
```
