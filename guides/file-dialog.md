# File Dialog

## Overview

This document explains how to open a file dialog and select files or directories. This functionality is implemented using PyQt's `QFileDialog` class. This document covers three methods: `open_file_dialog`, `save_file_dialog`, and `select_directory_dialog`.

## Method Descriptions

### `open_file_dialog`

Opens a dialog to open a file.

#### Parameters

- `dir` (str, optional): The directory where the dialog will initially open. Default is the current working directory.
- `filter` (str, optional): A string specifying the selectable file types. For example, it can be used like `"Text Files (*.txt);;All Files (*)"`.

#### Return Value

- `Optional[str]`: Returns the path of the selected file. Returns `None` if no file is selected.

#### Example

```python
app = Pyloid(app_name="Pyloid-App")
file_path = app.open_file_dialog(dir="/home/user", filter="Text Files (*.txt)")
if file_path:
    print("Selected file:", file_path)
```

### `save_file_dialog`

Opens a dialog to save a file.

#### Parameters

- `dir` (str, optional): The directory where the dialog will initially open. Default is the current working directory.
- `filter` (str, optional): A string specifying the savable file types. For example, it can be used like `"Text Files (*.txt);;All Files (*)"`.

#### Return Value

- `Optional[str]`: Returns the path of the selected file. Returns `None` if no file is selected.

#### Example

```python
app = Pyloid(app_name="Pyloid-App")
file_path = app.save_file_dialog(dir="/home/user", filter="Text Files (*.txt)")
if file_path:
    print("File will be saved to:", file_path)
```

### `select_directory_dialog`

Opens a dialog to select a directory.

#### Parameters

- `dir` (str, optional): The directory where the dialog will initially open. Default is the current working directory.

#### Return Value

- `Optional[str]`: Returns the path of the selected directory. Returns `None` if no directory is selected.

#### Example

```python
app = Pyloid(app_name="Pyloid-App")
directory_path = app.select_directory_dialog(dir="/home/user")
if directory_path:
    print("Selected directory:", directory_path)
```

## Note

These methods are implemented using PySide6's `QFileDialog` class. PyQt is a binding that allows the use of the Qt library in Python. `QFileDialog` provides standard dialogs for selecting files and directories.
