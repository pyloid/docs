# Tray

pylon-app make it easy to implement system tray functionality. This guide explains how to set up a tray icon, handle events, and add menu items.

## Setting up the Tray Icon

To set up a tray icon, use the `set_tray_icon` method:

```python
app.set_tray_icon("assets/icon.ico")
```

## Handling Tray Events

You can handle various click events on the tray icon. Use the `set_tray_actions` method to set up event handlers:

```python
app.set_tray_actions(
    {
        TrayEvent.DoubleClick: lambda: print("Tray icon was double-clicked."),
        TrayEvent.MiddleClick: lambda: print("Tray icon was middle-clicked."),
        TrayEvent.RightClick: lambda: print("Tray icon was right-clicked."),
        TrayEvent.LeftClick: lambda: print("Tray icon was left-clicked."),
    }
)
```

## Adding Tray Menu Items

You can add items to the context menu that appears when right-clicking the tray icon. Use the `set_tray_menu_items` method to set up menu items:

```python
app.set_tray_menu_items(
    [
        {"label": "Show Window", "callback": lambda: app.show_and_focus_main_window()},
        {"label": "Quit", "callback": lambda: app.quit()},
    ]
)
```

Each menu item is defined as a dictionary with `label` and `callback` keys.

## Complete Example

Here's a complete example implementing tray functionality:

```python
app = PylonApp("Pylon-App", single_instance=True)

if (is_production()):
    app.set_icon(os.path.join(get_production_path(), "icon.ico"))
    app.set_tray_icon(os.path.join(get_production_path(), "icon.ico"))
else:
    app.set_icon("assets/icon.ico")
    app.set_tray_icon("assets/icon.ico")

app.set_tray_actions(
    {
        TrayEvent.DoubleClick: lambda: print("Tray icon was double-clicked."),
        TrayEvent.MiddleClick: lambda: print("Tray icon was middle-clicked."),
        TrayEvent.RightClick: lambda: print("Tray icon was right-clicked."),
        TrayEvent.LeftClick: lambda: print("Tray icon was left-clicked."),
    }
)

app.set_tray_menu_items(
    [
        {"label": "Show Window", "callback": lambda: app.show_and_focus_main_window()},
        {"label": "Quit", "callback": lambda: app.quit()},
    ]
)
```

This example demonstrates setting up a tray icon, handling events, and adding menu items.