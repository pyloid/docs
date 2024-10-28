# Thread

We use PySide6's QThread class for multi-threaded operations.

## Basic QThread Usage

### 1. Inheriting QThread Class

```python
from PySide6.QtCore import QThread

class WorkerThread(QThread):
    def run(self):
        # Write your execution code here
        pass
```

### 2. Defining Signals (Optional)

```python
from PySide6.QtCore import QThread, Signal

class WorkerThread(QThread):
    progress = Signal(int)  # Signal for progress updates
    result = Signal(object)  # Signal for delivering results

    def run(self):
        # Emit signal during operation
        self.progress.emit(50)
        # Deliver operation result
        self.result.emit("Task completed")
```

### 3. Thread Usage Example

```python
def on_finished():
    print("Operation completed")

def on_progress(value):
    print(f"Progress: {value}%")


# Create thread instance
worker = WorkerThread()

worker.finished.connect(on_finished)  # Callback when task completes

worker.progress.connect(on_progress)  # Callback for progress updates

# Start thread
worker.start()
```

## Key Methods and Signals

### QThread Basic Methods

- `start()`: Start thread
- `quit()`: Request thread termination
- `wait()`: Wait until thread terminates
- `isRunning()`: Check if thread is running
- `terminate()`: Force thread termination (not recommended)

### Basic Signals

- `started`: Emitted when thread starts
- `finished`: Emitted when thread ends

## Important Notes

1. GUI updates should only be performed on the main thread.
2. Avoid using `terminate()` as it forces termination without resource cleanup.
3. Proper synchronization is needed when sharing data between threads.

## Example: Progress Display Operation

```python
from PySide6.QtCore import QThread, Signal
import time

class WorkerThread(QThread):
    progress = Signal(int)

    def run(self):
        for i in range(101):
            self.progress.emit(i)
            time.sleep(0.1)  # Simulating work

# Usage example
worker = WorkerThread()
worker.progress.connect(lambda v: print(f"Progress: {v}%"))
worker.finished.connect(lambda: print("Task completed!"))
worker.start()
```

This guide explains the basic methods of implementing multi-threading using QThread in PySide6.
In actual applications, please design and use appropriate signals and slots according to the characteristics of your tasks.
