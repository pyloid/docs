# Thread Safety

Pyloid is designed so that GUI functions, which must run only on the main thread in PySide6-based applications, can be called safely and asynchronously from other threads using **QEventLoop** and its own event loop mechanism.

This structure enables seamless integration with various Python server frameworks (such as FastAPI, Flask, Django, etc.), allowing events or commands from the server to be reflected in the GUI in real time.

```text
Server Thread
    |
    | execute_command()
    v
Pyloid (BrowserWindow)
    |
    | command_signal.emit()
    v
Main Thread (GUI)
    |
    | QEventLoop.exec()
    v
Actual GUI function execution
    |
    | result_signal.emit()
    v
Pyloid (BrowserWindow)
    |
    | Return result
    v
Server Thread
```

The core principles of Pyloid are as follows:

- **Thread communication using command_signal and result_signal**  
  When a GUI-related function is called from a separate thread, the command is sent to the main thread via a signal. The main thread processes the event using its own **QEventLoop**. Once the GUI function finishes execution, the result is sent back via another signal, so the calling thread can safely receive the result.

- **Asynchronous command processing and custom event loop**  
  For each command, Pyloid creates its own **QEventLoop** to wait asynchronously for the command to complete. This allows the server thread and GUI thread to communicate without blocking each other, maintaining GUI responsiveness.

- **Strong compatibility with server-client architectures**  
  Thanks to this structure, it is possible to safely implement various scenarios, such as launching a window directly from a server thread or dynamically controlling the GUI in response to web requests. For example, you can update the contents of a Pyloid window in real time upon receiving an HTTP request in a FastAPI server, or immediately reflect events from Flask in the GUI.
