# PyloidTimer Usage Guide

`PyloidTimer` is a convenient timer management class based on PySide6's QTimer. It allows you to easily create and manage various types of timers.

## Table of Contents
1. [Basic Usage](#basic-usage)
2. [Periodic Timers](#periodic-timers)
3. [Single-Shot Timers](#single-shot-timers)
4. [Timer Management](#timer-management)
5. [Precise Timers](#precise-timers)
6. [Advanced Usage](#advanced-usage)

## Basic Usage

First, create a `PyloidTimer` instance:

```python
from pyloid.timer import PyloidTimer

timer_manager = PyloidTimer()
```

## Periodic Timers

To start a timer that runs periodically, use the `start_periodic_timer` method:

```python
def print_hello():
    print("Hello!")

# Start a timer that prints "Hello!" every 2 seconds
timer_id = timer_manager.start_periodic_timer(2000, print_hello)
```

## Single-Shot Timers

To start a timer that runs only once, use the `start_single_shot_timer` method:

```python
def delayed_message():
    print("5 seconds have passed!")

# Start a single-shot timer that prints a message after 5 seconds
timer_id = timer_manager.start_single_shot_timer(5000, delayed_message)
```

## Timer Management

### Stopping a Timer

```python
# Stop a timer using its ID
timer_manager.stop_timer(timer_id)
```

### Checking Timer Activity

```python
if timer_manager.is_timer_active(timer_id):
    print("The timer is still running.")
else:
    print("The timer has stopped.")
```

### Checking Remaining Time

```python
remaining_time = timer_manager.get_remaining_time(timer_id)
if remaining_time is not None:
    print(f"{remaining_time}ms left until the timer fires.")
```

### Changing Timer Interval

```python
# Change the timer interval to 3 seconds
timer_manager.set_interval(timer_id, 3000)
```

## Precise Timers

For more precise timing, you can use precise timers:

```python
def precise_task():
    print("Executing precise task")

# Start a precise periodic timer with 100ms interval
precise_timer_id = timer_manager.start_precise_periodic_timer(100, precise_task)
```

Conversely, you can use less precise timers to save system resources:

```python
def coarse_task():
    print("Executing coarse task")

# Start a coarse periodic timer with 1-second interval
coarse_timer_id = timer_manager.start_coarse_periodic_timer(1000, coarse_task)
```

## Advanced Usage

### Using Lambda Functions

You can use lambda functions with timers to implement more complex logic:

```python
counter = 0

timer_id = timer_manager.start_periodic_timer(1000, lambda: (
    setattr(globals(), 'counter', counter + 1),
    print(f"Counter: {counter}")
)[1])
```

This example increments a counter and prints its value every second.

## Conclusion

`PyloidTimer` is a powerful tool for managing various timing requirements easily. It can be useful in a wide range of situations, from simple periodic tasks to tasks that require precise timing.