# Themes

## System Theme Integration

Pyloid can automatically detect and apply the user's system theme settings. Using CSS variables makes it easy to manage styles for light/dark modes.

### Basic Setup

```css
/* Light mode theme */
[data-pyloid-theme='light'] {
  --background-color: white;
  --font-color: #333333;
}

/* Dark mode theme */
[data-pyloid-theme='dark'] {
  --background-color: #333333;
  --font-color: white;
}

/* Applying CSS variables */
body {
  background-color: var(--background-color);
  color: var(--font-color);
}
```

### How It Works

1. The `data-pyloid-theme` attribute is automatically set to either 'light' or 'dark' based on the system's theme settings.
2. CSS variables are used to define styles for each theme.
3. Components reference these CSS variables to apply the styles.

### Example

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      [data-pyloid-theme='light'] {
        --background-color: white;
        --font-color: #333333;
      }

      [data-pyloid-theme='dark'] {
        --background-color: #333333;
        --font-color: white;
      }

      body {
        background-color: var(--background-color);
        color: var(--font-color);
      }
    </style>
  </head>

  <body>
    <div class="card">
      <h1>Dark Mode Test</h1>
      <p>
        This page automatically changes theme based on system dark mode settings.
      </p>
    </div>
  </body>
</html>
```

### Custom Theme Variables

Commonly used theme variables:

```css
[data-pyloid-theme='light'] {
  --primary-color: #007bff;
  --secondary-color: #6c757d;
  --background-color: white;
  --surface-color: #f8f9fa;
  --font-color: #333333;
  --border-color: #dee2e6;
}

[data-pyloid-theme='dark'] {
  --primary-color: #0d6efd;
  --secondary-color: #6c757d;
  --background-color: #333333;
  --surface-color: #424242;
  --font-color: white;
  --border-color: #495057;
}
```

## Manual Theme Switching

If needed, you can manually switch themes using JavaScript:

```javascript
// Switch to dark mode
document.documentElement.setAttribute('data-pyloid-theme', 'dark');

// Switch to light mode
document.documentElement.setAttribute('data-pyloid-theme', 'light');
```

## Detecting Theme Changes

Pyloid emits a `themeChange` custom event when the theme changes. You can use this event to perform necessary actions when the theme changes.

### Registering Event Listener

```javascript
document.addEventListener('themeChange', (e) => {
    console.log('Theme changed:', e.detail.theme); // 'light' or 'dark'

    updateTheme(e.detail.theme);
});
```

### Usage Examples

1. Changing images based on theme:
```javascript
function updateTheme(theme) {
    const logo = document.querySelector('.logo');
    if (theme === 'dark') {
        logo.src = '/images/logo-dark.png';
    } else {
        logo.src = '/images/logo-light.png';
    }
}
```

2. Sending theme information in API calls:
```javascript
function updateTheme(theme) {
    // Save user preferences
    fetch('/api/user/preferences', {
        method: 'POST',
        body: JSON.stringify({ theme: theme }),
        headers: {
            'Content-Type': 'application/json'
        }
    });
}
```

### Important Notes

- The `themeChange` event fires on initial load and when the system theme changes.
- `e.detail.theme` contains either 'light' or 'dark' value.

Using these event listeners enables dynamic UI/UX implementation based on theme changes.

