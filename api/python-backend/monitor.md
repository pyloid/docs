# Monitor

## Overview
The Monitor class provides functionality to manage and manipulate information about computer monitors. This class uses PySide6's QScreen object to access various properties and functions of the monitor.

## Constructor

### `__init__(self, index: int, screen: QScreen)`
Initializes a Monitor object.

- **Parameters**:
  - `index` (int): The index of the monitor
  - `screen` (QScreen): The QScreen object corresponding to the monitor

## Methods

### `capture(self, save_path: str, x: Optional[int] = None, y: Optional[int] = None, width: Optional[int] = None, height: Optional[int] = None) -> Optional[str]`
Captures the monitor screen.

- **Parameters**:
  - `save_path` (str): Path to save the captured image
  - `x` (Optional[int]): Starting x-coordinate for capture (default: None)
  - `y` (Optional[int]): Starting y-coordinate for capture (default: None)
  - `width` (Optional[int]): Width of the area to capture (default: None)
  - `height` (Optional[int]): Height of the area to capture (default: None)
- **Returns**: 
  - str: Path of the saved image
  - None: If capture fails

### `info(self) -> dict`
Returns a dictionary containing all information about the monitor.

- **Returns**: dict: Dictionary containing monitor information

### `is_primary(self) -> bool`
Checks if the current monitor is the primary monitor.

- **Returns**: bool: True if primary monitor, False otherwise

### `size(self) -> dict`
Returns the size of the monitor.

- **Returns**: dict: Dictionary with 'width' and 'height' keys

### `geometry(self) -> dict`
Returns the geometric information of the monitor.

- **Returns**: dict: Dictionary with 'x', 'y', 'width', 'height' keys

### `available_geometry(self) -> dict`
Returns the geometric information of the available monitor area.

- **Returns**: dict: Dictionary with 'x', 'y', 'width', 'height' keys

### `available_size(self) -> dict`
Returns the size of the available monitor area.

- **Returns**: dict: Dictionary with 'width' and 'height' keys

### `virtual_geometry(self) -> dict`
Returns the geometric information of the monitor on the virtual desktop.

- **Returns**: dict: Dictionary with 'x', 'y', 'width', 'height' keys

### `virtual_size(self) -> dict`
Returns the size of the monitor on the virtual desktop.

- **Returns**: dict: Dictionary with 'width' and 'height' keys

### `available_virtual_geometry(self) -> dict`
Returns the geometric information of the available virtual desktop area.

- **Returns**: dict: Dictionary with 'x', 'y', 'width', 'height' keys

### `available_virtual_size(self) -> dict`
Returns the size of the available virtual desktop area.

- **Returns**: dict: Dictionary with 'width' and 'height' keys

### `physical_size(self) -> dict`
Returns the physical size of the monitor.

- **Returns**: dict: Dictionary with 'width' and 'height' keys

### `depth(self) -> int`
Returns the color depth of the monitor.

- **Returns**: int: Color depth of the monitor

### `device_pixel_ratio(self) -> float`
Returns the device pixel ratio of the monitor.

- **Returns**: float: Device pixel ratio

### `logical_dots_per_inch(self) -> float`
Returns the logical DPI of the monitor.

- **Returns**: float: Logical DPI

### `logical_dots_per_inch_x(self) -> float`
Returns the horizontal logical DPI of the monitor.

- **Returns**: float: Horizontal logical DPI

### `logical_dots_per_inch_y(self) -> float`
Returns the vertical logical DPI of the monitor.

- **Returns**: float: Vertical logical DPI

### `orientation(self) -> str`
Returns the orientation of the monitor.

- **Returns**: str: Monitor orientation ('Portrait', 'Landscape', etc.)

### `physical_dots_per_inch(self) -> float`
Returns the physical DPI of the monitor.

- **Returns**: float: Physical DPI

### `physical_dots_per_inch_x(self) -> float`
Returns the horizontal physical DPI of the monitor.

- **Returns**: float: Horizontal physical DPI

### `physical_dots_per_inch_y(self) -> float`
Returns the vertical physical DPI of the monitor.

- **Returns**: float: Vertical physical DPI

### `refresh_rate(self) -> float`
Returns the refresh rate of the monitor.

- **Returns**: float: Monitor refresh rate (Hz)

### `manufacturer(self) -> str`
Returns the manufacturer of the monitor.

- **Returns**: str: Monitor manufacturer name

### `model(self) -> str`
Returns the model of the monitor.

- **Returns**: str: Monitor model name

### `name(self) -> str`
Returns the name of the monitor.

- **Returns**: str: Monitor name

### `serial_number(self) -> str`
Returns the serial number of the monitor.

- **Returns**: str: Monitor serial number

### `geometry_changed(self, callback: Callable)`
Sets a callback for the monitor geometry change event.

- **Parameters**:
  - `callback` (Callable): Function to be called when geometry changes

### `orientation_changed(self, callback: Callable)`
Sets a callback for the monitor orientation change event.

- **Parameters**:
  - `callback` (Callable): Function to be called when orientation changes

### `refresh_rate_changed(self, callback: Callable)`
Sets a callback for the monitor refresh rate change event.

- **Parameters**:
  - `callback` (Callable): Function to be called when refresh rate changes
