---
version: v0.36.4
category: API
title: Synopsis
source_url: 'https://github.com/atom/electron/blob/master/docs/api/synopsis.md'
---

# Synopsis

All of [Node.js's built-in modules](http://nodejs.org/api/) are available in
Electron and third-party node modules also fully supported as well (including
the [native modules](http://electron.atom.io/docs/v0.36.4/tutorial/using-native-node-modules)).

Electron also provides some extra built-in modules for developing native
desktop applications. Some modules are only available in the main process, some
are only available in the renderer process (web page), and some can be used in
both processes.

The basic rule is: if a module is [GUI][gui] or low-level system related, then
it should be only available in the main process. You need to be familiar with
the concept of [main process vs. renderer process][main-process] scripts to be
able to use those modules.

The main process script is just like a normal Node.js script:

```javascript
const electron = require('electron');
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;

var window = null;

app.on('ready', function() {
  window = new BrowserWindow({width: 800, height: 600});
  window.loadURL('https://github.com');
});
```

The renderer process is no different than a normal web page, except for the
extra ability to use node modules:

```html
<!DOCTYPE html>
<html>
<body>
<script>
  const remote = require('electron').remote;
  console.log(remote.app.getVersion());
</script>
</body>
</html>
```

To run your app, read [Run your app](http://electron.atom.io/docs/v0.36.4/tutorial/quick-start#run-your-app).

## Destructuring assignment

If you are using CoffeeScript or Babel, you can also use
[destructuring assignment][desctructuring-assignment] to make it easier to use
built-in modules:

```javascript
const {app, BrowserWindow} = require('electron')
```

However if you are using plain JavaScript, you have to wait until Chrome fully
supports ES6.

## Disable old styles of using built-in modules

Before v0.35.0, all built-in modules have to be used in the form of
`require('module-name')`, though it has [many disadvantages][issue-387], we are
still supporting it for compatibility with old apps.

To disable the old styles completely, you can set the
`ELECTRON_HIDE_INTERNAL_MODULES` environment variable:

```javascript
process.env.ELECTRON_HIDE_INTERNAL_MODULES = 'true'
```

Or call the `hideInternalModules` API:

```javascript
require('electron').hideInternalModules()
```

[gui]: https://en.wikipedia.org/wiki/Graphical_user_interface
[main-process]: http://electron.atom.io/docs/v0.36.4/tutorial/quick-start#the-main-process
[desctructuring-assignment]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
[issue-387]: https://github.com/atom/electron/issues/387
