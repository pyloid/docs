## Pyloid

Pyloid is a high-level desktop application framework built on top of PySide6. It simplifies window creation, system tray management, clipboard interaction, RPC communication, file watching, and more. All functions in Pyloid are thread-safe, meaning they can be safely executed from threads other than the main thread.

---

### Initialization

```python
from pyloid import Pyloid

app = Pyloid(app_name="MyApp", single_instance=True)
```

**Parameters**

- **app_name** : `str`
    Name of the application (used for auto-start and single-instance logic).
- **single_instance** : `bool`, optional, default: `True`
    Whether to enforce a single running instance.

**Returns**

- `Pyloid`: The initialized application instance.

---

### Window Management

#### `create_window`

```python
window = app.create_window(
    title="Main Window",
    width=1024,
    height=768,
    x=100,
    y=100,
    frame=True,
    context_menu=True,
    dev_tools=True,
    rpc=rpc
)
```

**Parameters**

- **title** : `str`, optional, default: "pylon app"
    Title of the window.
- **width** : `int`, optional, default: `800`
    Width of the window.
- **height** : `int`, optional, default: `600`
    Height of the window.
- **x** : `int`, optional, default: `200`
    X position of the window.
- **y** : `int`, optional, default: `200`
    Y position of the window.
- **frame** : `bool`, optional, default: `True`
    Whether the window has a visible frame.
- **context_menu** : `bool`, optional, default: `False`
    Whether to enable right-click context menu.
- **dev_tools** : `bool`, optional, default: `False`
    Whether to enable developer tools.
- **rpc** : `Optional[PyloidRPC]`, optional
    RPC instance for JavaScript communication.

**Returns**

- `BrowserWindow`: The created browser window.

#### `get_windows`

```python
windows = app.get_windows()
print(windows)
```

**Returns**

- `Dict[str, BrowserWindow]`: Dictionary of all open windows.

#### `get_window_by_id`

```python
window = app.get_window_by_id("your-window-id")
```

**Parameters**

- **window_id** : `str`
    ID of the window to retrieve.

**Returns**

- `Optional[BrowserWindow]`: Window object or None.

#### `show_main_window`, `focus_main_window`, `show_and_focus_main_window`, `close_all_windows`, `quit`

Each of these methods takes no parameters and returns `None`.

---

### Tray System

#### `set_tray_icon`

```python
app.set_tray_icon("icon.png")
```

**Parameters**

- **tray_icon_path** : `str`
    Path to the tray icon file.

**Returns**

- `bool`: True if successful.

#### `set_tray_menu_items`

```python
app.set_tray_menu_items([
    {"label": "Open", "callback": lambda: app.show_main_window()},
    {"label": "Quit", "callback": app.quit}
])
```

**Parameters**

- **tray_menu_items** : `List[Dict[str, Union[str, Callable]]]`
    Menu items to add to the tray context menu.

**Returns**

- `bool`: True if successful.

#### `show_notification`

```python
app.show_notification("Hello", "This is a notification.")
```

**Parameters**

- **title** : `str`
- **message** : `str`

**Returns**

- `bool`: True if successful.

---

### Clipboard

#### `set_clipboard_text`

```python
app.set_clipboard_text("Copied text")
```

**Parameters**

- **text** : `str`

**Returns**

- `None`

#### `get_clipboard_text`

```python
text = app.get_clipboard_text()
```

**Returns**

- `str`: Clipboard text.

#### `set_clipboard_image`

```python
app.set_clipboard_image("image.png")
```

**Parameters**

- **image** : `Union[str, bytes, os.PathLike]`
    Image file path or data.

**Returns**

- `None`

#### `get_clipboard_image`

```python
img = app.get_clipboard_image()
```

**Returns**

- `Optional[QImage]`: Clipboard image object.

---

### Autostart

#### `set_auto_start`

```python
app.set_auto_start(True)
```

**Parameters**

- **enable** : `bool`

**Returns**

- `Union[bool, None]`: True if enabled, False if disabled, None if unsupported.

#### `is_auto_start`

```python
print(app.is_auto_start())
```

**Returns**

- `bool`: Whether auto-start is active.

---

### File Watcher

#### `watch_file`, `watch_directory`, `stop_watching`

Each takes a `str` path and returns `bool`.

#### `get_watched_paths`, `get_watched_files`, `get_watched_directories`

```python
paths = app.get_watched_paths()
```

**Returns**

- `List[str]`: Watched paths or files or directories.

#### `remove_all_watched_paths`

```python
app.remove_all_watched_paths()
```

**Returns**

- `None`

#### `set_file_change_callback`, `set_directory_change_callback`

**Parameters**

- **callback** : `Callable[[str], None]`

**Returns**

- `None`

---

### File Dialogs

#### `open_file_dialog`

```python
file_path = app.open_file_dialog(dir="/home/user", filter="Images (*.png *.jpg)")
```

**Parameters**

- **dir** : `Optional[str]`
    Initial directory.
- **filter** : `Optional[str]`
    Filter for file types.

**Returns**

- `Optional[str]`: Selected file path or None.

#### `save_file_dialog`

```python
save_path = app.save_file_dialog(dir="/home/user", filter="Text Files (*.txt)")
```

Same parameters and return type as `open_file_dialog`.

#### `select_directory_dialog`

```python
dir_path = app.select_directory_dialog(dir="/home/user")
```

**Parameters**

- **dir** : `Optional[str]`
    Initial directory.

**Returns**

- `Optional[str]`: Selected directory path or None.

---

### Platform Dirs

Each returns a `str` path to the respective directory:

- `user_data_dir()`
- `site_data_dir()`
- `user_cache_dir()`
- `user_log_dir()`
- `user_documents_dir()`
- `user_downloads_dir()`
- `user_pictures_dir()`
- `user_videos_dir()`
- `user_music_dir()`
- `user_desktop_dir()`
- `user_runtime_dir()`

---

### Store API

#### `store`

```python
store = app.store("settings.json")
store.set("theme", "dark")
print(store.get("theme"))
```

**Parameters**

- **path** : `str`
    File name of the store.
- **user_data_dir** : `bool`, optional, default: `True`
    Whether to place the file inside the user data directory.

**Returns**

- `Store`: Store object supporting `.set()` and `.get()`.

---

### Run the App

```python
app.run()
```

**Returns**

- `None`: Starts the application event loop.