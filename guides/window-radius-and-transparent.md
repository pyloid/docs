# Window Border Radius and Transparency

Pyloid allows you to easily set the border radius and transparency of windows. These features enable you to create various custom UI designs, especially frameless and transparent windows.

## Basic Setup

To set up window border radius and transparency, follow these steps:

1. Use the `frame=False` option when creating a window to remove the default frame.
2. Use the `transparent=True` option
3. Use HTML/CSS to set the desired border radius and transparency.

```python
window = app.create_window(
    title="My Transparent Window",
    frame=False,
    transparent=True, # Required for a transparent window
    width=500,
    height=500
)
```

## Setting Border Radius

Use the CSS `border-radius` property to shape your window into a circle, oval, or rounded corners:

```html
<style>
  html,
  body {
    margin: 0;
    background: transparent;
  }
  #main {
    border-radius: 9999px; /* Circular window */
  }
</style>
```

You can set different border-radius values to create various shapes:

- `border-radius: 10px;` - Slightly rounded corners
- `border-radius: 20px 50px;` - Various corner radii
- `border-radius: 50%;` - Perfect circle

### Important Note

**Important**: The `border-radius` property won't work if applied directly to the `body` tag. You must apply it to a child element (e.g., div) inside the `body`. For example:

```html
<!-- Won't work -->
<style>
  html,
  body {
    margin: 0;
    background: transparent;
    border-radius: 9999px;
  }
</style>

<!-- Correct method -->
<style>
  html,
  body {
    margin: 0;
    background: transparent;
  }
  #main {
    width: 100vw;
    height: 100vh;
    border-radius: 9999px;
  }
</style>
<body>
  <div id="main"></div>
</body>
```

## Setting Transparency

Use the CSS `rgba()` color value to set the window's transparency:

```html
<style>
  #main {
    background: rgba(
      255,
      255,
      255,
      0.3
    ); /* White background with 30% opacity */
  }
</style>
```

The transparency value is set by the last parameter (alpha channel) in rgba:

- `1.0` - Completely opaque
- `0.5` - 50% transparent
- `0.0` - Completely transparent

### Critical Requirement

**Important**: For window transparency to work properly, you must set `background: transparent;` on both the `html` and `body` elements. This is essential for the transparent parts of your window to actually appear transparent rather than having a solid background. Example:

```html
<style>
  html,
  body {
    margin: 0;
    padding: 0;
    background: transparent; /* This is required for transparency to work */
  }
  #main {
    /* Your custom styling with rgba background */
    background: rgba(255, 255, 255, 0.3);
  }
</style>
```

Without setting `background: transparent;` on these elements, your window will appear with a solid background regardless of the rgba values you set on child elements.

## Setting Drag Region

For frameless transparent or rounded windows, you need to use the `data-pyloid-drag-region` attribute to make them draggable:

```html
<div
  id="main"
  data-pyloid-drag-region
>
  Hello World!
</div>
```

## Complete Example

![window-radius-and-transparent image](/.gitbook/assets/window-radius-and-transparent.png)

Here's a complete example code for creating a circular semi-transparent window:

```python
from pyloid import Pyloid

app = Pyloid(app_name="pyloid-app")

window = app.create_window(
    "border-radius and transparent", frame=False, width=500, height=500
)

html = """
<!DOCTYPE html>
<html>
  <head>
    <style>
      html,
      body {
        margin: 0;
        padding: 0;
        background: transparent;
      }
      #main {
        width: 100vw;
        height: 100vh;
        background: rgba(255, 255, 255, 0.3);
        border-radius: 9999px;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    </style>
  </head>
  <body>
    <div
      id="main"
      data-pyloid-drag-region
    >
      Hello World!
    </div>
  </body>
</html>
"""

window.load_html(html)
window.show_and_focus()

app.run()
```

This example demonstrates the following features:

- Creating a frameless window (frame=False).
- Enabling window-level transparency (transparent=True).
- Setting a semi-transparent background (`background: rgba(255, 255, 255, 0.3)`)
- Setting a draggable area (`data-pyloid-drag-region`)

Combine these settings to create various window designs.
