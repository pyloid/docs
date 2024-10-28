# Window Position

### 1. Using parameters when creating a window

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Pyloid-Window", x=100, y=100)
```

### 2. Using the `set_position` method

The window position is determined by the `x` and `y` parameters.

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Pyloid-Window")

window.set_position(x=100, y=100)
```

### 3. Using the `set_position_by_anchor` method

The window position is determined by the `anchor` parameter.

The position is set based on the available screen space (excluding the taskbar).

Available anchor positions:
- `top`
- `left`
- `right`
- `bottom`
- `top-left`
- `top-right`
- `bottom-left`
- `bottom-right`
- `center`

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Pyloid-Window")

window.set_position_by_anchor("center")
```
