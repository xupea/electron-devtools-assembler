Electron DevTools Installer
---------------------------

![CircleCI](https://img.shields.io/circleci/build/github/xupea/electron-devtools-installer?style=for-the-badge)
[![npm](https://img.shields.io/npm/v/electron-devtools-assembler?style=for-the-badge)](https://www.npmjs.com/package/electron-devtools-assembler)
![npm](https://img.shields.io/npm/dt/electron-devtools-assembler?style=for-the-badge)
[![license](https://img.shields.io/github/license/xupea/electron-devtools-installer.svg?maxAge=2592000&style=for-the-badge)](https://github.com/xupea/electron-devtools-installer/blob/master/LICENSE)
[![CFA Enabled](https://img.shields.io/badge/CFA-Enabled-success?style=for-the-badge)](https://github.com/continuousauth)

This is an easy way to install DevTool extensions into Electron.  You shouldn't
have to mess around with downloading the extension, finding the right folder and
then configuring the path for everyone's machines.

## Why

1. The origin electron-devtools-installer is not maintained anymore

2. Manifest V2 will stop working for extensions

3. Electron has limited support for Chrome extension(eg. chrome.scripting)

This repo uses the fixed version for each extension instead of downloading them from the Chrome Store for two reasons:

- The Chrome Store version may not work

- No access to the Google domain

## Install

```
npm install electron-devtools-assembler --save-dev
```
or
```
yarn add electron-devtools-assembler -D
```

## Usage
All you have to do now is this in the **main** process of your application.

```js
import installExtension, { REDUX_DEVTOOLS } from 'electron-devtools-assembler';
// Or if you can not use ES6 imports
/**
const { default: installExtension, REACT_DEVELOPER_TOOLS } = require('electron-devtools-assembler');
*/
const { app } = require('electron');

app.whenReady().then(() => {
    installExtension(REDUX_DEVTOOLS)
        .then((name) => console.log(`Added Extension:  ${name}`))
        .catch((err) => console.log('An error occurred: ', err));
});
```
To install multiple extensions, `installExtension` takes an array.

## What extensions can I use?

Technically you can use whatever extension you want.  Simply find the ChromeStore ID
of the extension you want to install, and call `installExtension('YOUR_ID_HERE')`.  We
offer a few extension ID's inside the package so you can easily import them to install without
having to find them yourselves.

```js
import installExtension, {
  EMBER_INSPECTOR, REACT_DEVELOPER_TOOLS,
  BACKBONE_DEBUGGER, JQUERY_DEBUGGER,
  ANGULAR_DEVTOOLS, VUEJS_DEVTOOLS,
  REDUX_DEVTOOLS, MOBX_DEVTOOLS, 
  APOLLO_DEVELOPER_TOOLS,
} from 'electron-devtools-assembler';
```

## How does it work?

Well, you know those steps over in the [Electron Docs](https://github.com/electron/electron/blob/master/docs/tutorial/devtools-extension.md)
that involve downloading, copying, checking paths, Etc.

This does all of that for you, it downloads the chrome extension directly from
the Chrome WebStore.  Then it extracts it to your applications `userData` directory
before loading it into Electron.


## Harmless warnings and errors

```shell
(node:27182) ExtensionLoadWarning: Warnings loading extension at .../Electron/extensions/lmhkpmbekcpmknklioeibfkpmmfibljd:
  Manifest version 2 is deprecated, and support will be removed in 2023. See https://developer.chrome.com/blog/mv2-transition/ for more details.
  Permission 'notifications' is unknown or URL pattern is malformed.
  Permission 'contextMenus' is unknown or URL pattern is malformed.
```

```shell
[27182:0327/232739.839908:ERROR:CONSOLE(2)] "Electron sandboxed_renderer.bundle.js script failed to run", source: node:electron/js2c/sandbox_bundle (2)
[27182:0327/232739.839937:ERROR:CONSOLE(2)] "TypeError: object null is not iterable (cannot read property Symbol(Symbol.iterator))", source: node:electron/js2c/sandbox_bundle (2)
```

## Maintenance

| Extension              | Version | Electron |      |
| ---------------------- | ------- | -------- | ---- |
| EMBER_INSPECTOR        | 4.9.1   | 23.0.0   | ✅    |
| REACT_DEVELOPER_TOOLS  | 4.24.7  | 23.0.0   | ✅    |
| BACKBONE_DEBUGGER      | 0.4.1   | 23.0.0   | ✅    |
| JQUERY_DEBUGGER        | 0.1.3.2 | 23.0.0   | ✅    |
| ANGULAR_DEVTOOLS       | 1.0.7   | 23.0.0   | ✅    |
| VUEJS_DEVTOOLS         | 6.5.0   | 23.0.0   | ✅    |
| REDUX_DEVTOOLS         | 3.0.19  | 23.0.0   | ✅    |
| APOLLO_DEVELOPER_TOOLS | 4.1.4   | 23.0.0   | ✅    |
| MOBX_DEVTOOLS          | 0.9.26  | 23.0.0   | ✅    |

## Resource

https://www.electronjs.org/docs/latest/api/extensions#chromedevtoolsinspectedwindow

https://developer.chrome.com/docs/extensions/migrating/mv2-sunset/


License
-------

The MIT License (MIT)

Copyright (c) 2023 Peter Xu

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
