---
version: v0.36.0
category: API
title: 'Global Shortcut'
source_url: 'https://github.com/atom/electron/blob/master/docs/api/global-shortcut.md'
---

# global-shortcut

The `global-shortcut` module can register/unregister a global keyboard shortcut
with the operating system so that you can customize the operations for various
shortcuts.

**Note:** The shortcut is global; it will work even if the app does
not have the keyboard focus. You should not use this module until the `ready`
event of the app module is emitted.

```javascript
const electron = require('electron');
const app = electron.app;
const globalShortcut = electron.globalShortcut;

app.on('ready', function() {
  // Register a 'ctrl+x' shortcut listener.
  var ret = globalShortcut.register('ctrl+x', function() {
    console.log('ctrl+x is pressed');
  });

  if (!ret) {
    console.log('registration failed');
  }

  // Check whether a shortcut is registered.
  console.log(globalShortcut.isRegistered('ctrl+x'));
});

app.on('will-quit', function() {
  // Unregister a shortcut.
  globalShortcut.unregister('ctrl+x');

  // Unregister all shortcuts.
  globalShortcut.unregisterAll();
});
```

## Methods

The `global-shortcut` module has the following methods:

### `globalShortcut.register(accelerator, callback)`

* `accelerator` [Accelerator](http://electron.atom.io/docs/v0.36.0/api/accelerator)
* `callback` Function

Registers a global shortcut of `accelerator`. The `callback` is called when
the registered shortcut is pressed by the user. Returns `true` if the shortcut
`accelerator` was registered, `false` otherwise. For example, the specified
`accelerator` has already been registered by another caller or other native
applications.

### `globalShortcut.isRegistered(accelerator)`

* `accelerator` [Accelerator](http://electron.atom.io/docs/v0.36.0/api/accelerator)

Returns `true` or `false` depending on whether the shortcut `accelerator` is
registered.

### `globalShortcut.unregister(accelerator)`

* `accelerator` [Accelerator](http://electron.atom.io/docs/v0.36.0/api/accelerator)

Unregisters the global shortcut of `accelerator`.

### `globalShortcut.unregisterAll()`

Unregisters all of the global shortcuts.
