# Serve Frontend(Static Files)

Pyloid provides functionality to easily serve web-based UIs. Using the `pyloid_serve` function from the `pyloid.serve` module, you can serve static files from a local HTTP server. The server uses dynamic port allocation by default, automatically finding an available port on your system.

## Basic Usage

```python
from pyloid import Pyloid
from pyloid.serve import pyloid_serve

app = Pyloid("Pyloid-App")

url = pyloid_serve("dist-front")  # Serve static files from dist-front folder

window = app.create_window("Pyloid-App")
window.load_url(url)
window.show_and_focus()
```

## Function Details

```python
pyloid_serve(directory: str, port: Optional[int] = None) -> str
```

### Parameters

- `directory` (str): Path to the static file directory to serve
- `port` (int, optional): Server port (default: None - will use dynamic port allocation to automatically find an available port)

### Returns

- `str`: URL of the started server (e.g. "http://127.0.0.1:65421")

## How It Works

The `pyloid_serve` function internally uses Python's `http.server` module to run a lightweight HTTP server in a separate thread. When no port is specified, it utilizes dynamic port allocation to find an available port on your system, ensuring that the server can start without port conflicts. This server runs as a daemon thread, so it terminates when the main application exits.
