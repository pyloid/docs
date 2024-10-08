# Autostart

You can use the `app.set_auto_start()` function to set whether the application should start automatically when the user logs in.

```python
app.set_auto_start(True)  # Enable auto-start
app.set_auto_start(False)  # Disable auto-start
```

This function takes a boolean value as an argument. If the value is `True`, the application will start automatically when the user logs in. If the value is `False`, the application will not start automatically.

## Notes

- `set_auto_start(True)` only works in production environments.
- `set_auto_start(False)` works in all environments.
- Calling `set_auto_start(True)` in a non-production environment will print a warning message and return `None`.

## Checking Auto-start Status

You can use the `app.is_auto_start()` function to check the current auto-start setting status.

```python
is_auto_start = app.is_auto_start()
print(is_auto_start)  # Prints True or False
```

This function returns `True` if auto-start is enabled, and `False` otherwise.
