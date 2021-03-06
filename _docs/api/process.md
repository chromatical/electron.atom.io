---
version: v1.2.5
category: API
redirect_from:
    - /docs/v0.24.0/api/process/
    - /docs/v0.25.0/api/process/
    - /docs/v0.26.0/api/process/
    - /docs/v0.27.0/api/process/
    - /docs/v0.28.0/api/process/
    - /docs/v0.29.0/api/process/
    - /docs/v0.30.0/api/process/
    - /docs/v0.31.0/api/process/
    - /docs/v0.32.0/api/process/
    - /docs/v0.33.0/api/process/
    - /docs/v0.34.0/api/process/
    - /docs/v0.35.0/api/process/
    - /docs/v0.36.0/api/process/
    - /docs/v0.36.3/api/process/
    - /docs/v0.36.4/api/process/
    - /docs/v0.36.5/api/process/
    - /docs/v0.36.6/api/process/
    - /docs/v0.36.7/api/process/
    - /docs/v0.36.8/api/process/
    - /docs/v0.36.9/api/process/
    - /docs/v0.36.10/api/process/
    - /docs/v0.36.11/api/process/
    - /docs/v0.37.0/api/process/
    - /docs/v0.37.1/api/process/
    - /docs/v0.37.2/api/process/
    - /docs/v0.37.3/api/process/
    - /docs/v0.37.4/api/process/
    - /docs/v0.37.5/api/process/
    - /docs/v0.37.6/api/process/
    - /docs/v0.37.7/api/process/
    - /docs/v0.37.8/api/process/
    - /docs/latest/api/process/
source_url: 'https://github.com/electron/electron/blob/master/docs/api/process.md'
excerpt: "Extensions to process object."
title: "process"
sort_title: "process"
---

# process

> Extensions to process object.

The `process` object is extended in Electron with following APIs:

## Events

### Event: 'loaded'

Emitted when Electron has loaded its internal initialization script and is
beginning to load the web page or the main script.

It can be used by the preload script to add removed Node global symbols back to
the global scope when node integration is turned off:

```javascript
// preload.js
const _setImmediate = setImmediate;
const _clearImmediate = clearImmediate;
process.once('loaded', () => {
  global.setImmediate = _setImmediate;
  global.clearImmediate = _clearImmediate;
});
```

## Properties

### `process.noAsar`

Setting this to `true` can disable the support for `asar` archives in Node's
built-in modules.

### `process.type`

Current process's type, can be `"browser"` (i.e. main process) or `"renderer"`.

### `process.versions.electron`

Electron's version string.

### `process.versions.chrome`

Chrome's version string.

### `process.resourcesPath`

Path to the resources directory.

### `process.mas`

For Mac App Store build, this property is `true`, for other builds it is
`undefined`.

### `process.windowsStore`

If the app is running as a Windows Store app (appx), this property is `true`,
for otherwise it is `undefined`.

### `process.defaultApp`

When app is started by being passed as parameter to the default app, this
property is `true` in the main process, otherwise it is `undefined`.

## Methods

The `process` object has the following method:

### `process.crash()`

Causes the main thread of the current process crash.

### `process.hang()`

Causes the main thread of the current process hang.

### `process.setFdLimit(maxDescriptors)` _macOS_ _Linux_

* `maxDescriptors` Integer

Sets the file descriptor soft limit to `maxDescriptors` or the OS hard
limit, whichever is lower for the current process.

### `process.getProcessMemoryInfo()`

Returns an object giving memory usage statistics about the current process. Note
that all statistics are reported in Kilobytes.

* `workingSetSize` - The amount of memory currently pinned to actual physical
  RAM.
* `peakWorkingSetSize` - The maximum amount of memory that has ever been pinned
  to actual physical RAM.
* `privateBytes` - The amount of memory not shared by other processes, such as
  JS heap or HTML content.
* `sharedBytes` - The amount of memory shared between processes, typically
  memory consumed by the Electron code itself

### `process.getSystemMemoryInfo()`

Returns an object giving memory usage statistics about the entire system. Note
that all statistics are reported in Kilobytes.

* `total` - The total amount of physical memory in Kilobytes available to the
  system.
* `free` - The total amount of memory not being used by applications or disk
  cache.

On Windows / Linux:

* `swapTotal` - The total amount of swap memory in Kilobytes available to the
  system.
* `swapFree` - The free amount of swap memory in Kilobytes available to the
  system.
