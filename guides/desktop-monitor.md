# Desktop Monitor

## Overview

You can obtain monitor objects using the `app.get_primary_monitor()` or `app.get_all_monitors()` methods. Through these monitor objects, you can perform various functions and utilize several methods of the `Monitor` object to query or modify the properties and states of the monitor.

## Methods

#### `capture(save_path: str, x: Optional[int] = None, y: Optional[int] = None, width: Optional[int] = None, height: Optional[int] = None)`

- **Description**: Captures the entire desktop screen.
- **Parameters**:
  - `save_path` (str): Path to save the captured image.
  - `x`, `y`, `width`, `height` (int, optional): Coordinates and size of the area to capture.
- **Return Value**: Returns the path of the saved image. Returns `None` if an error occurs.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  save_path = monitor.capture("screenshot.png")
  print(f"Screenshot saved at: {save_path}")
  ```

#### `info() -> dict[str, Any]`

- **Description**: Returns all information about the monitor.
- **Return Value**: A dictionary containing all monitor information.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  info = monitor.info()
  print("Monitor Info:", info)
  ```

#### `is_primary() -> bool`

- **Description**: Checks if the monitor is the primary monitor.
- **Return Value**: `True` if it's the primary monitor, `False` otherwise.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_all_monitors()[1]
  is_primary = monitor.is_primary()
  print(f"Is primary monitor: {is_primary}") # False
  ```

#### `size() -> dict[str, int]`

- **Description**: Returns the size of the monitor.
- **Return Value**: A dictionary containing the width and height of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  size = monitor.size()
  print("Monitor Size:", size)
  ```

#### `geometry() -> dict[str, int]`

- **Description**: Returns the x, y, width, height information of the monitor.
- **Return Value**: A dictionary containing the x, y, width, height information of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  geometry = monitor.geometry()
  print("Monitor Geometry:", geometry)
  ```

#### `available_geometry() -> dict[str, int]`

- **Description**: Returns the available x, y, width, height information of the monitor.
- **Return Value**: A dictionary containing the x, y, width, height information of the monitor, excluding system UI elements.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  available_geometry = monitor.available_geometry()
  print("Available Geometry:", available_geometry)
  ```

#### `available_size() -> dict[str, int]`

- **Description**: Returns the available size of the monitor.
- **Return Value**: A dictionary containing the width and height of the monitor, excluding system UI elements.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  available_size = monitor.available_size()
  print("Available Size:", available_size)
  ```

#### `virtual_geometry() -> dict[str, int]`

- **Description**: Returns the virtual x, y, width, height information of the monitor.
- **Return Value**: A dictionary containing the combined x, y, width, height information of all monitors in a multi-monitor setup.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  virtual_geometry = monitor.virtual_geometry()
  print("Virtual Geometry:", virtual_geometry)
  ```

#### `virtual_size() -> dict[str, int]`

- **Description**: Returns the virtual size of the monitor.
- **Return Value**: A dictionary containing the combined width and height of all monitors in a multi-monitor setup.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  virtual_size = monitor.virtual_size()
  print("Virtual Size:", virtual_size)
  ```

#### `available_virtual_geometry() -> dict[str, int]`

- **Description**: Returns the available virtual x, y, width, height information of the monitor.
- **Return Value**: A dictionary containing the virtual x, y, width, height information, excluding system UI elements.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  available_virtual_geometry = monitor.available_virtual_geometry()
  print("Available Virtual Geometry:", available_virtual_geometry)
  ```

#### `available_virtual_size() -> dict[str, int]`

- **Description**: Returns the available virtual size of the monitor.
- **Return Value**: A dictionary containing the virtual size, excluding system UI elements.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  available_virtual_size = monitor.available_virtual_size()
  print("Available Virtual Size:", available_virtual_size)
  ```

#### `physical_size() -> dict[str, float]`

- **Description**: Returns the physical size of the monitor.
- **Return Value**: A dictionary containing the actual physical width and height of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  physical_size = monitor.physical_size()
  print("Physical Size:", physical_size)
  ```

#### `depth() -> int`

- **Description**: Returns the color depth of the monitor.
- **Return Value**: The color depth of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  depth = monitor.depth()
  print("Color Depth:", depth)
  ```

#### `device_pixel_ratio() -> float`

- **Description**: Returns the device pixel ratio of the monitor.
- **Return Value**: The device pixel ratio of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  device_pixel_ratio = monitor.device_pixel_ratio()
  print("Device Pixel Ratio:", device_pixel_ratio)
  ```

#### `logical_dots_per_inch() -> float`

- **Description**: Returns the logical DPI of the monitor.
- **Return Value**: The logical DPI of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  logical_dpi = monitor.logical_dots_per_inch()
  print("Logical DPI:", logical_dpi)
  ```

#### `logical_dots_per_inch_x() -> float`

- **Description**: Returns the logical DPI on the X-axis of the monitor.
- **Return Value**: The logical DPI on the X-axis of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  logical_dpi_x = monitor.logical_dots_per_inch_x()
  print("Logical DPI X:", logical_dpi_x)
  ```

#### `logical_dots_per_inch_y() -> float`

- **Description**: Returns the logical DPI on the Y-axis of the monitor.
- **Return Value**: The logical DPI on the Y-axis of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  logical_dpi_y = monitor.logical_dots_per_inch_y()
  print("Logical DPI Y:", logical_dpi_y)
  ```

#### `orientation() -> str`

- **Description**: Returns the orientation of the monitor.
- **Return Value**: The orientation of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  orientation = monitor.orientation()
  print("Orientation:", orientation)
  ```

#### `physical_dots_per_inch() -> float`

- **Description**: Returns the physical DPI of the monitor.
- **Return Value**: The physical DPI of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  physical_dpi = monitor.physical_dots_per_inch()
  print("Physical DPI:", physical_dpi)
  ```

#### `physical_dots_per_inch_x() -> float`

- **Description**: Returns the physical DPI on the X-axis of the monitor.
- **Return Value**: The physical DPI on the X-axis of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  physical_dpi_x = monitor.physical_dots_per_inch_x()
  print("Physical DPI X:", physical_dpi_x)
  ```

#### `physical_dots_per_inch_y() -> float`

- **Description**: Returns the physical DPI on the Y-axis of the monitor.
- **Return Value**: The physical DPI on the Y-axis of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  physical_dpi_y = monitor.physical_dots_per_inch_y()
  print("Physical DPI Y:", physical_dpi_y)
  ```

#### `refresh_rate() -> float`

- **Description**: Returns the refresh rate of the monitor.
- **Return Value**: The refresh rate of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  refresh_rate = monitor.refresh_rate()
  print("Refresh Rate:", refresh_rate)
  ```

#### `manufacturer() -> str`

- **Description**: Returns the manufacturer of the monitor.
- **Return Value**: The manufacturer of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  manufacturer = monitor.manufacturer()
  print("Manufacturer:", manufacturer)
  ```

#### `model() -> str`

- **Description**: Returns the model of the monitor.
- **Return Value**: The model of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  model = monitor.model()
  print("Model:", model)
  ```

#### `name() -> str`

- **Description**: Returns the name of the monitor.
- **Return Value**: The name of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  name = monitor.name()
  print("Name:", name)
  ```

#### `serial_number() -> str`

- **Description**: Returns the serial number of the monitor.
- **Return Value**: The serial number of the monitor.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  monitor = app.get_primary_monitor()
  serial_number = monitor.serial_number()
  print("Serial Number:", serial_number)
  ```

#### `geometry_changed(callback: Callable)`

- **Description**: Registers a callback to be called when the monitor's geometry changes.
- **Parameters**:
  - `callback` (Callable): Function to be called when the geometry changes.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  def on_geometry_changed():
      print("Geometry changed!")
  monitor = app.get_primary_monitor()
  monitor.geometry_changed(on_geometry_changed)
  ```

#### `orientation_changed(callback: Callable)`

- **Description**: Registers a callback to be called when the monitor's orientation changes.
- **Parameters**:
  - `callback` (Callable): Function to be called when the orientation changes.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  def on_orientation_changed():
      print("Orientation changed!")
  monitor = app.get_primary_monitor()
  monitor.orientation_changed(on_orientation_changed)
  ```

#### `refresh_rate_changed(callback: Callable)`

- **Description**: Registers a callback to be called when the monitor's refresh rate changes.
- **Parameters**:
  - `callback` (Callable): Function to be called when the refresh rate changes.
- **Example**:
  ```python
  app = Pyloid("Pyloid-App")
  def on_refresh_rate_changed():
      print("Refresh rate changed!")
  monitor = app.get_primary_monitor()
  monitor.refresh_rate_changed(on_refresh_rate_changed)
  ```

The `Monitor` class provides various other methods for querying monitor properties. Each method returns a specific attribute of the monitor, and usage examples are similar to those shown above.
