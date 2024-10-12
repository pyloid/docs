# File Watcher

The File Watcher provides functionality to monitor changes in specific files or directories. This allows you to receive automatic notifications when files or directories are modified.

## Basic Usage

### Start Watching a File

To monitor changes in a specific file, use the following:

```python
result = app.watch_file("/path/to/file.txt")
if result:
    print("File watching started")
else:
    print("Failed to start file watching")
```

### Start Watching a Directory

To monitor changes in a specific directory, use the following:

```python
result = app.watch_directory("/path/to/directory")
if result:
    print("Directory watching started")
else:
    print("Failed to start directory watching")
```

### Set File Change Callback

You can set a callback function to be executed when a file is changed:

```python
def on_file_changed(path):
    print(f"File has been changed: {path}")

app.set_file_change_callback(on_file_changed)
```

### Set Directory Change Callback

You can set a callback function to be executed when a directory is changed:

```python
def on_directory_changed(path):
    print(f"Directory has been changed: {path}")

app.set_directory_change_callback(on_directory_changed)
```

### Stop Watching

To stop watching a specific file or directory, use the following:

```python
result = app.stop_watching("/path/to/file_or_directory")
if result:
    print("Watching stopped successfully")
else:
    print("Failed to stop watching")
```

### Check Watched Paths

To check all currently watched paths (files and directories), use the following:

```python
watched_paths = app.get_watched_paths()
print("All watched paths:", watched_paths)
```

### Get Only Watched Files

```python
watched_files = app.get_watched_files()
print("Watched files:", watched_files)
```

### Get Only Watched Directories

```python
watched_directories = app.get_watched_directories()
print("Watched directories:", watched_directories)
```

### Remove All Watched Paths

```python
app.remove_all_watched_paths()
print("All watched paths have been removed.")
```

## Usage Example

Here's a comprehensive example of using the File Watcher:

```python
# Start watching file and directory
app.watch_file("/path/to/file.txt")
app.watch_directory("/path/to/directory")

# Define callback functions
def on_file_changed(path):
    print(f"File changed: {path}")

def on_directory_changed(path):
    print(f"Directory changed: {path}")

# Set callback functions
app.set_file_change_callback(on_file_changed)
app.set_directory_change_callback(on_directory_changed)

# Check watched paths
print("Watched paths:", app.get_watched_paths())
print("Watched files:", app.get_watched_files())
print("Watched directories:", app.get_watched_directories())

# Stop watching a specific path
app.stop_watching("/path/to/file.txt")

# Remove all watched paths
app.remove_all_watched_paths()
```

## Precautions

- The File Watcher uses system resources, so use it only when necessary and clean up properly when finished.
- Watching a large number of files or directories can impact system performance, so use caution.
- Some file systems or operating systems may not detect certain types of changes.

This guide should help you understand the basic usage and advanced features of the File Watcher. If you have any additional questions or need further assistance, please don't hesitate to ask.
