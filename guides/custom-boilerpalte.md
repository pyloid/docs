# Creating a Custom Boilerplate

You can create a boilerplate using your preferred frontend framework instead of the provided boilerplate.

## Method

Choose your desired frontend framework. e.g., React, Vue, Svelte, Angular, etc.

## Example (React)

### 1. Create a React project

```bash
npm create vite@latest
# Select React
```

### 2. Modify the index.html file

#### Add Security Policy to index.html (Optional)

{% code title="index.html" %}
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <script src="qrc:///qtwebchannel/qwebchannel.js"></script>
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pyloid</title>
    <!-- Add security policy (Optional) -->
    <meta
      http-equiv="Content-Security-Policy"
      content="default-src 'self'; script-src 'self' qrc://*; img-src 'self' data:; style-src 'self' 'unsafe-inline';"
    />
    <!------------------------------------>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```
{% endcode %}

### 3. Modify the main.jsx/tsx file

Proceed with rendering after the pylonReady event occurs to ensure rendering takes place after Pyloid's functions are loaded.

```tsx
document.addEventListener('pyloidReady', () => {
  // DOM rendering code
});
```

This ensures that rendering proceeds after Pyloid's functions are loaded.

{% code title="main.tsx" %}
```tsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import App from './App.tsx';
import './index.css';

document.addEventListener('pyloidReady', () => {
  createRoot(document.getElementById('root')!).render(
    <StrictMode>
      <App />
    </StrictMode>
  );
});
```
{% endcode %}

### 4. Modify the vite.config.ts file

Specify the build folder as the path where the built html file is generated.

{% code title="vite.config.ts" %}
```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  base: './',
  build: {
    outDir: 'build',
  },
});
```
{% endcode %}

### 5. Modify package.json

Add scripts for development and build tasks for each OS.
Also, add concurrently and run-script-os to devDependencies.

{% hint style="info" %}
If you're using a package manager like pnpm, yarn, or bun, you'll need to change the scripts to match your package manager.
{% endhint %}

{% hint style="warning" %}
We set windows: python / linux: python3 / macos: python3 as the default Python command. So if your computer uses a different default command like py/python/python3, you'll need to modify it.
{% endhint %}

{% code title="package.json" %}
```json
{
  // ...

  "scripts": {
    "dev": "run-script-os",
    "dev:windows": "concurrently --raw --names \"front,pyloid\" \"npm run vite\" \".\\venv-pyloid\\Scripts\\python .\\src-pyloid\\main.py\"",
    "dev:linux": "concurrently --raw --names \"front,pyloid\" \"npm run vite\" \"./venv-pyloid/bin/python ./src-pyloid/main.py\"",
    "dev:macos": "concurrently --raw --names \"front,pyloid\" \"npm run vite\" \"./venv-pyloid/bin/python ./src-pyloid/main.py\"",
    "vite": "vite",
    "build": "tsc -b && vite build && run-script-os",
    "build:windows": ".\\venv-pyloid\\Scripts\\pyinstaller build-windows.spec",
    "build:linux": "./venv-pyloid/bin/pyinstaller build-linux.spec",
    "build:macos": "./venv-pyloid/bin/pyinstaller build-macos.spec",
    "init": "npm install && run-script-os",
    "init:windows": "python -m venv venv-pyloid && .\\venv-pyloid\\Scripts\\pip install -r requirements.txt",
    "init:linux": "python3 -m venv venv-pyloid && ./venv-pyloid/bin/pip install -r requirements.txt",
    "init:macos": "python3 -m venv venv-pyloid && ./venv-pyloid/bin/pip install -r requirements.txt"
  },

  // ...

  "devDependencies": {
    "concurrently": "^9.0.1",
    "run-script-os": "^1.1.6"
  }
}
```
{% endcode %}

### 6. Add requirements.txt to the root directory

Add the pyloid package and pyinstaller package.

{% code title="requirements.txt" %}
```
pyloid
pyinstaller
```
{% endcode %}

### 7. Add pyinstaller spec files

Add pyinstaller spec files to the root path to build the project into an exe file.

![file tree](/.gitbook/assets/boilerplate1.png)

This is the file path image used here.
There's a src-pyloid folder in the root path, and a main.py file inside it.

{% hint style="warning" %}
If your project file path is different, you'll need to modify the spec file accordingly.
(Icon path, build html path, Python file path)
{% endhint %}

{% tabs %}
{% tab title="build-windows.spec" %}
```python
# -*- mode: python ; coding: utf-8 -*-
block_cipher = None

a = Analysis(['src-pyloid/main.py'],
            pathex=[],
            binaries=[],
            datas=[('src-pyloid/icons/', 'icons/'),
            ('build/', 'build/'),
            ],
            hiddenimports=[],
            hookspath=[],
            hooksconfig={},
            runtime_hooks=[],
            excludes=['PySide6.QtQml', 'PySide6.QtTest', 'PySide6.Qt3D', 'PySide6.QtSensors', 'PySide6.QtCharts', 'PySide6.QtGraphs', 'PySide6.QtDataVisualization', 'PySide6.QtQuick', 'PySide6.QtDesigner', 'PySide6.QtUiTools', 'PySide6.QtHelp'],
            win_no_prefer_redirects=False,
            win_private_assemblies=False,
            cipher=block_cipher,
            noarchive=False)

pyz = PYZ(a.pure, a.zipped_data,
          cipher=block_cipher)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='pyloid-app',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
    icon=['src-pyloid/icons/icon.ico'],
)

coll = COLLECT(
    exe,
    a.binaries,
    a.zipfiles,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='pyloid-app'
)
```
{% endtab %}

{% tab title="build-linux.spec" %}
```python
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None

a = Analysis(['src-pylon/main.py'],
            pathex=[],
            binaries=[],
            datas=[('src-pyloid/icons/', 'icons/'),
            ('build/', 'build/'),
            ],
            hiddenimports=[],
            excludes=['PySide6.QtQml', 'PySide6.QtTest', 'PySide6.Qt3D', 'PySide6.QtSensors', 'PySide6.QtCharts', 'PySide6.QtGraphs', 'PySide6.QtDataVisualization', 'PySide6.QtQuick', 'PySide6.QtDesigner', 'PySide6.QtUiTools', 'PySide6.QtHelp'],
            hookspath=[],
            hooksconfig={},
            runtime_hooks=[],
            win_no_prefer_redirects=False,
            win_private_assemblies=False,
            cipher=block_cipher,
            noarchive=False)

pyz = PYZ(a.pure, a.zipped_data,
          cipher=block_cipher)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='pyloid-app',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
    icon=['src-pyloid/icons/icon.png'],
)

coll = COLLECT(
    exe,
    a.binaries,
    a.zipfiles,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='pyloid-app'
)
```
{% endtab %}

{% tab title="build-macos.spec" %}
```python
# -*- mode: python ; coding: utf-8 -*-


a = Analysis(
    ['src-pyloid/main.py'],
    pathex=[],
    binaries=[],
    datas=[('src-pyloid/icons/', 'icons/'),
             ('build/', 'build/'),
             ],
    hiddenimports=['PySide6.QtWebEngineCore'],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=['PySide6.QtQml', 'PySide6.QtTest', 'PySide6.Qt3D', 'PySide6.QtSensors', 'PySide6.QtCharts', 'PySide6.QtGraphs', 'PySide6.QtDataVisualization', 'PySide6.QtQuick', 'PySide6.QtDesigner', 'PySide6.QtUiTools', 'PySide6.QtHelp'],
    noarchive=False,
    optimize=0,
)
pyz = PYZ(a.pure)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='pyloid-app',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
)
coll = COLLECT(
    exe,
    a.binaries,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='pyloid-app',
)
app = BUNDLE(
    coll,
    name='pyloid-app.app',
    icon='src-pyloid/icons/icon.icns',
    bundle_identifier=None,
)
```
{% endtab %}
{% endtabs %}

### 8. Add icons (Optional)

Add icon files if needed.

![icon path](/.gitbook/assets/boilerplate1.png)

And you need to modify the spec file to match that path.

### 9. Run

```bash
npm run dev
```

Run the project to test.

### 10. Build

```bash
npm run build
```

Build the project to test.