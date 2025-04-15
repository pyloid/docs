### baseAPI

The `BaseAPI` class provides asynchronous methods to interact with the Pyloid backend via `window.__PYLOID__`. All methods automatically wait for Pyloid initialization before executing.
`baseAPI` is an singleton instance of the `BaseAPI` class.

#### Methods

1. **getData**
   - **Description**: Retrieves generic data passed from the Pyloid backend during initialization.
   - **Returns**: `Promise<any>` - A promise that resolves with the data.
   - **Example**:
     ```javascript
     baseAPI.getData().then(data => console.log(data));
     ```

2. **getWindowId**
   - **Description**: Gets the unique identifier for the current window.
   - **Returns**: `Promise<string>` - A promise that resolves with the window ID string.
   - **Example**:
     ```javascript
     baseAPI.getWindowId().then(id => console.log(`Window ID: ${id}`));
     ```

3. **getWindowProperties**
   - **Description**: Retrieves properties associated with the current window.
   - **Returns**: `Promise<WindowProperties>` - A promise that resolves with an object containing window properties.
   - **Example**:
     ```javascript
     baseAPI.getWindowProperties().then(props => console.log(props));
     ```

4. **close**
   - **Description**: Closes the current window.
   - **Returns**: `Promise<void>` - A promise that resolves when the close operation is initiated.
   - **Example**:
     ```javascript
     baseAPI.close().then(() => console.log('Window closed.'));
     ```

5. **hide**
   - **Description**: Hides the current window.
   - **Returns**: `Promise<void>` - A promise that resolves when the hide operation is initiated.
   - **Example**:
     ```javascript
     baseAPI.hide().then(() => console.log('Window hidden.'));
     ```

6. **show**
   - **Description**: Shows the current window if it is hidden.
   - **Returns**: `Promise<void>` - A promise that resolves when the show operation is initiated.
   - **Example**:
     ```javascript
     baseAPI.show().then(() => console.log('Window shown.'));
     ```

7. **focus**
   - **Description**: Brings the current window to the foreground and gives it focus.
   - **Returns**: `Promise<void>` - A promise that resolves when the focus operation is initiated.
   - **Example**:
     ```javascript
     baseAPI.focus().then(() => console.log('Window focused.'));
     ```

8. **showAndFocus**
   - **Description**: Shows the window (if hidden) and brings it to the foreground with focus.
   - **Returns**: `Promise<void>` - A promise that resolves when the operation is initiated.
   - **Example**:
     ```javascript
     baseAPI.showAndFocus().then(() => console.log('Window shown and focused.'));
     ```

9. **fullscreen**
   - **Description**: Makes the current window fullscreen.
   - **Returns**: `Promise<void>` - A promise that resolves when the fullscreen operation is initiated.
   - **Example**:
     ```javascript
     baseAPI.fullscreen().then(() => console.log('Window is now fullscreen.'));
     ```

10. **toggleFullscreen**
    - **Description**: Toggles the fullscreen state of the current window.
    - **Returns**: `Promise<void>` - A promise that resolves when the toggle operation is initiated.
    - **Example**:
      ```javascript
      baseAPI.toggleFullscreen().then(() => console.log('Fullscreen toggled.'));
      ```

11. **minimize**
    - **Description**: Minimizes the current window.
    - **Returns**: `Promise<void>` - A promise that resolves when the minimize operation is initiated.
    - **Example**:
      ```javascript
      baseAPI.minimize().then(() => console.log('Window minimized.'));
      ```

12. **maximize**
    - **Description**: Maximizes the current window.
    - **Returns**: `Promise<void>` - A promise that resolves when the maximize operation is initiated.
    - **Example**:
      ```javascript
      baseAPI.maximize().then(() => console.log('Window maximized.'));
      ```

13. **unmaximize**
    - **Description**: Restores the window from a maximized state.
    - **Returns**: `Promise<void>` - A promise that resolves when the unmaximize operation is initiated.
    - **Example**:
      ```javascript
      baseAPI.unmaximize().then(() => console.log('Window restored from maximized state.'));
      ```

14. **toggleMaximize**
    - **Description**: Toggles the maximized state of the current window.
    - **Returns**: `Promise<void>` - A promise that resolves when the toggle operation is initiated.
    - **Example**:
      ```javascript
      baseAPI.toggleMaximize().then(() => console.log('Maximize toggled.'));
      ```

15. **isFullscreen**
    - **Description**: Checks if the current window is in fullscreen mode.
    - **Returns**: `Promise<boolean>` - A promise that resolves with true if fullscreen, false otherwise.
    - **Example**:
      ```javascript
      baseAPI.isFullscreen().then(isFullscreen => console.log(`Is fullscreen: ${isFullscreen}`));
      ```

16. **isMaximized**
    - **Description**: Checks if the current window is maximized.
    - **Returns**: `Promise<boolean>` - A promise that resolves with true if maximized, false otherwise.
    - **Example**:
      ```javascript
      baseAPI.isMaximized().then(isMaximized => console.log(`Is maximized: ${isMaximized}`));
      ```

17. **setTitle**
    - **Description**: Sets the title of the current window.
    - **Parameters**: `title: string` - The new title for the window.
    - **Returns**: `Promise<void>` - A promise that resolves when the title is set.
    - **Example**:
      ```javascript
      baseAPI.setTitle('New Title').then(() => console.log('Title set.'));
      ```

18. **setSize**
    - **Description**: Sets the size (width and height) of the current window.
    - **Parameters**: 
      - `width: number` - The desired width in pixels.
      - `height: number` - The desired height in pixels.
    - **Returns**: `Promise<void>` - A promise that resolves when the size is set.
    - **Example**:
      ```javascript
      baseAPI.setSize(1024, 768).then(() => console.log('Window size set.'));
      ```

19. **setPosition**
    - **Description**: Sets the position (x and y coordinates) of the current window.
    - **Parameters**: 
      - `x: number` - The desired x-coordinate.
      - `y: number` - The desired y-coordinate.
    - **Returns**: `Promise<void>` - A promise that resolves when the position is set.
    - **Example**:
      ```javascript
      baseAPI.setPosition(100, 100).then(() => console.log('Window position set.'));
      ```

20. **setFrame**
    - **Description**: Sets whether the window should have a standard OS frame.
    - **Parameters**: `frame: boolean` - True to show the frame, false to hide it.
    - **Returns**: `Promise<void>` - A promise that resolves when the frame state is set.
    - **Example**:
      ```javascript
      baseAPI.setFrame(true).then(() => console.log('Frame set.'));
      ```

21. **getFrame**
    - **Description**: Gets the current frame state of the window.
    - **Returns**: `Promise<boolean>` - A promise that resolves with true if the frame is visible, false otherwise.
    - **Example**:
      ```javascript
      baseAPI.getFrame().then(frame => console.log(`Frame visible: ${frame}`));
      ```

22. **getTitle**
    - **Description**: Gets the current title of the window.
    - **Returns**: `Promise<string>` - A promise that resolves with the window title string.
    - **Example**:
      ```javascript
      baseAPI.getTitle().then(title => console.log(`Window title: ${title}`));
      ```

23. **getSize**
    - **Description**: Gets the current size (width and height) of the window.
    - **Returns**: `Promise<Size>` - A promise that resolves with an object containing the width and height.
    - **Example**:
      ```javascript
      baseAPI.getSize().then(size => console.log(`Window size: ${size.width}x${size.height}`));
      ```

24. **getPosition**
    - **Description**: Gets the current position (x and y coordinates) of the window.
    - **Returns**: `Promise<Position>` - A promise that resolves with an object containing the x and y coordinates.
    - **Example**:
      ```javascript
      baseAPI.getPosition().then(position => console.log(`Window position: (${position.x}, ${position.y})`));
      ```

25. **setClipboardText**
    - **Description**: Sets the system clipboard text content.
    - **Parameters**: `text: string` - The text to write to the clipboard.
    - **Returns**: `Promise<void>` - A promise that resolves when the clipboard text is set.
    - **Example**:
      ```javascript
      baseAPI.setClipboardText('Hello, World!').then(() => console.log('Clipboard text set.'));
      ```

26. **getClipboardText**
    - **Description**: Gets the current text content from the system clipboard.
    - **Returns**: `Promise<string>` - A promise that resolves with the clipboard text.
    - **Example**:
      ```javascript
      baseAPI.getClipboardText().then(text => console.log(`Clipboard text: ${text}`));
      ```

27. **setClipboardImage**
    - **Description**: Sets the system clipboard image content from a file path.
    - **Parameters**: 
      - `imagePath: string` - The path to the image file.
      - `format: string` - The format of the image (e.g., 'png', 'jpeg').
    - **Returns**: `Promise<void>` - A promise that resolves when the clipboard image is set.
    - **Example**:
      ```javascript
      baseAPI.setClipboardImage('/path/to/image.png', 'png').then(() => console.log('Clipboard image set.'));
      ```

28. **getClipboardImage**
    - **Description**: Gets the current image content from the system clipboard.
    - **Returns**: `Promise<string>` - A promise that resolves with the clipboard image data.
    - **Example**:
      ```javascript
      baseAPI.getClipboardImage().then(imageData => console.log(`Clipboard image data: ${imageData}`));
      ```

29. **quit**
    - **Description**: Quits the entire application.
    - **Returns**: `Promise<void>` - A promise that resolves when the quit operation is initiated.
    - **Example**:
      ```javascript
      baseAPI.quit().then(() => console.log('Application quit.'));
      ```

30. **getPlatform**
    - **Description**: Gets the underlying operating system platform.
    - **Returns**: `Promise<Platform>` - A promise that resolves with the platform name ('windows', 'linux', or 'macos').
    - **Example**:
      ```javascript
      baseAPI.getPlatform().then(platform => console.log(`Platform: ${platform}`));
      ```

31. **isProduction**
    - **Description**: Checks if the application is running in production mode.
    - **Returns**: `Promise<boolean>` - A promise that resolves with true if in production, false otherwise.
    - **Example**:
      ```javascript
      baseAPI.isProduction().then(isProd => console.log(`Is production: ${isProd}`));
      ```

32. **getProductionPath**
    - **Description**: Resolves a relative path to an absolute path within the application's production build directory.
    - **Parameters**: `path: string` - The relative path within the production build.
    - **Returns**: `Promise<string>` - A promise that resolves with the absolute path.
    - **Example**:
      ```javascript
      baseAPI.getProductionPath('assets/image.png').then(absPath => console.log(`Absolute path: ${absPath}`));
      ```

33. **getRpcUrl**
    - **Description**: Retrieves the RPC URL.
    - **Returns**: `Promise<string>` - A promise that resolves with the RPC URL.
    - **Example**:
      ```javascript
      baseAPI.getRpcUrl().then(url => console.log(`RPC URL: ${url}`));
      ```

### Usage Example

```javascript
import { baseAPI } from 'pyloid-js';

// Get the title of the window and print it to the console
baseAPI.getTitle().then(title => console.log(title));

// Set the size of the window to 1024x768
baseAPI.setSize(1024, 768).then(() => console.log('Window size set.'));
```
