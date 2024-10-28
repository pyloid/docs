# Splash Screen

Provides splash screen functionality displayed during application loading.

## Basic Usage

### 1. Splash Screen Setup

#### Static Image Splash Screen

```python
app = Pyloid(app_name="Pyloid-App")

window = app.create_window("Splash Screen Example")
window.set_static_image_splash_screen(image_path="./assets/loading.png")
```

#### Parameters

- `image_path`: Image file path
- `close_on_load`: Auto-close on page load completion (default: True)
- `stay_on_top`: Always display on top (default: True)
- `clickable`: Allow closing by click (default: True)
- `position`: Splash screen position (default: "center")
  - Supported positions: "center", "top-left", "top-right", "bottom-left", "bottom-right"

#### GIF Splash Screen

```python
window.set_gif_splash_screen(gif_path="./assets/loading.gif")
```

#### Parameters

- `gif_path`: GIF file path
- `close_on_load`: Auto-close on page load completion (default: True)
- `stay_on_top`: Always display on top (default: True)
- `clickable`: Allow closing by click (default: True)
- `position`: Splash screen position (default: "center")
  - Supported positions: "center", "top-left", "top-right", "bottom-left", "bottom-right"

### 2. Splash Screen Control

#### Manually Close Splash Screen

```python
window.close_splash_screen()
```

#### Thread Control Example

```python
from PySide6.QtCore import QThread
import time

# ... assuming window object is already created

class SplashWorkerThread(QThread):
    def run(self):
        # Write initialization code here
        time.sleep(2)  # Example: 2 second delay

def finish_callback():
    window.close_splash_screen()
    window.show_and_focus()

# Create and start thread
splash_worker = SplashWorkerThread()
splash_worker.finished.connect(finish_callback)
splash_worker.start()
```

## Usage Scenarios

1. **Initial Loading Screen**
   - Loading resources at application start
   - Database connection
   - External API initialization

2. **Display During Long Operations**
   - Large file processing
   - Network operations
   - Complex calculations

## Precautions

1. Optimize GIF files with appropriate size and quality
2. Manual splash screen closure required when `close_on_load=False`
3. Consider exception handling when using threads
