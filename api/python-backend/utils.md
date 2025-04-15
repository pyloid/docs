# Utility Functions

Pyloid provides several utility functions to help with resource path resolution, environment detection, platform identification, and networking.

---

### `get_production_path(path: Optional[str] = None) -> Optional[str]`

Constructs the absolute path to a resource file, adjusting based on the execution environment.

- In a production environment (e.g., when packaged with PyInstaller or Nuitka), it prepends the application's base directory to the provided relative path.  
- If no path is provided, it returns the base path itself.
- In a development environment (regular Python script), it simply returns the provided path as is. If no path is provided, it returns `None`.

**Parameters**

- `path` (`Optional[str]`, optional): The relative path to the resource file from the application's root directory. Defaults to `None`.

**Returns**

- `Optional[str]`:  
  - If in production: The absolute path to the resource file (or the base path if `path` is `None`).  
  - If not in production: The original `path` value passed to the function.

**Examples**

```python
from pyloid.utils import get_production_path, is_production

# Not in production
get_production_path("assets/icon.ico")
# 'assets/icon.ico'
get_production_path()
# None

# In production (e.g., PyInstaller bundle, sys._MEIPASS = '/tmp/_MEIabcde')
get_production_path("assets/icon.ico")  # '/tmp/_MEIabcde/assets/icon.ico'
get_production_path()                   # '/tmp/_MEIabcde'
```

---

### `is_production() -> bool`

Checks if the current environment is a production environment (e.g., PyInstaller or Nuitka bundle).

- Returns `True` if running in a production environment, otherwise `False`.

**Returns**

- `bool`: `True` if in a production environment, `False` otherwise.

**Examples**

```python
from pyloid.utils import is_production

if is_production():
    print("Running in production environment.")
else:
    print("Not in production environment.")
```

---

### `get_platform() -> str`

Returns the name of the current system's platform.

- Uses `platform.system()` to determine the OS.
- Returns one of: `"windows"`, `"macos"`, `"linux"`.

**Returns**

- `"windows"` | `"macos"` | `"linux"`

**Examples**

```python
from pyloid.utils import get_platform

platform_name = get_platform()
print(platform_name)  # e.g., "windows"
```

---

### `get_absolute_path(path: str) -> str`

Returns the absolute path of the given relative path.

**Parameters**

- `path` (`str`): The relative path to convert.

**Returns**

- `str`: The absolute path.

**Examples**

```python
from pyloid.utils import get_absolute_path

absolute_path = get_absolute_path("assets/icon.ico")
print(absolute_path)
# e.g., 'C:/Users/aaaap/Documents/pyloid/pyloid/assets/icon.ico'
```

---

### `get_free_port() -> int`

Finds and returns an available random network port number from the operating system.

- Creates a socket, binds to port `0` (let OS choose), retrieves the port, and closes the socket.
- Note: The port may be reassigned to another process after this function returns, so use it quickly.

**Returns**

- `int`: An available network port number (typically in the range 1024-65535).

**Examples**

```python
from pyloid.utils import get_free_port

port = get_free_port()
print(f"Found available port: {port}")

# Example: Start a web server on the found port
import http.server
server = http.server.HTTPServer(('localhost', port), http.server.SimpleHTTPRequestHandler)
```
