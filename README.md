# 🗡 ffxiv-overlay-api 🛡

![BADGE](https://img.shields.io/github/workflow/status/dsrkafuu/ffxiv-overlay-api/npm-publish)
![BADGE](https://img.shields.io/npm/v/ffxiv-overlay-api)
![BADGE](https://img.shields.io/npm/dm/ffxiv-overlay-api)
![BADGE](https://img.shields.io/npm/l/ffxiv-overlay-api)

Build your own modern FFXIV overlay with npm.

This library needs to be used along with [ngld/OverlayPlugin](https://github.com/ngld/OverlayPlugin).

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Options](#options)
- [API](#api)
- [Development](#development)
- [Contributon](#contributon)
- [Annotations](#annotations)

## Installation

You can install it from [npm registry](https://www.npmjs.com/package/ffxiv-overlay-api):

```bash
npm install ffxiv-overlay-api --save
```

Or import the library from jsDelivr CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/ffxiv-overlay-api@3.5/lib/overlay.min.js"></script>
<script>
  const overlay = new OverlayAPI({
    extendData: true,
    silentMode: false,
  });
</script>
```

## Usage

After installation, you can import the library:

```js
import OverlayAPI from 'ffxiv-overlay-api';
const overlay = new OverlayAPI();
```

Note that this library only works in browser.

You can also pass options to constructor (default option below):

```js
const overlay = new OverlayAPI({
  extendData: true,
  silentMode: false,
});
```

Then you can add bunch of different listeners.

```js
const overlay = new OverlayAPI();
overlay.addListener('CombatData', (data) => {
  console.log('listener of `CombatData`', data);
});
overlay.addListener('ChangeZone', (data) => {
  console.log('listener of `ChangeZone`', data);
});
```

Call this function once you’re done adding all of your listeners:

```js
overlay.startEvent();
```

Once this function has been called, OverlayPlugin will start sending events. Some events will be raised immediately with current state information like `ChangeZone` or `ChangePrimaryPlayer`.

After that, put the URL of your overlay into OverlayPlugin, or use the WebSocket URL when enabled. Checkout the [index.html](https://github.com/dsrkafuu/ffxiv-overlay-api/blob/master/test/index.html) for example usage, you can download this file and load it from the OverlayPlugin. Enable WebSocked in your plugin and add `?OVERLAY_WS=ws://127.0.0.1:[port]/ws` or `?HOST_PORT=ws://127.0.0.1:[port]` after you overlay URL to access the WebSocket server.

Checkout [Development](#development) section for more details.

## Options

| Option       | Default | Description                                             |
| ------------ | ------- | ------------------------------------------------------- |
| `extendData` | `true`  | Parse and add cleaner data to listeners of `CombatData` |
| `silentMode` | `false` | For production use, do not log all API stats info       |
| `seperateLB` | `false` | Separate Limit Break data from Combatant data           |

## API

You can find all events available in <https://ngld.github.io/OverlayPlugin/devs/event_types>.

### `OverlayAPI.addListener(event, cb)`

add an event listener

- `@param {EventType} event` event to listen
- `@param {Function} cb` callback function

### `OverlayAPI.removeListener(event, cb)`

remove a listener

- `@param {EventType} event` event type which listener belongs to
- `@param {Function} cb` function which listener to remove

### `OverlayAPI.removeAllListener(event)`

remove all listener of one event type

- `@param {EventType} event` event type which listener belongs to

### `OverlayAPI.getAllListener(event)`

get all listeners of a event

- `@param {EventType} event` event type which listener belongs to
- `@return {Array<Function>}`

### `OverlayAPI.startEvent()`

start listening event

### `OverlayAPI.endEncounter()`

ends current encounter and save it

- `@return {Promise<any>}`

### `OverlayAPI.callHandler(msg)`

this function allows you to call an overlay handler, these handlers are declared by Event Sources, either built into OverlayPlugin or loaded through addons like Cactbot

- `@param {HandlerMessage} msg` message send to OverlayPlugin
- `@return {Promise<EventMessage>}`

### `OverlayAPI.simulateData(msg)`

simulate triggering event once

- `@param {EventMessage} msg` data same as those from OverlayPluginApi like in <https://github.com/dsrkafuu/ffxiv-overlay-api/tree/master/test>

## Development

Clone this repo, then:

```bash
npm install
npm start
```

You can access the test overlay at `http://localhost:5000/test/`, `http://localhost:5000/test/?OVERLAY_WS=ws://127.0.0.1:[port]/ws` or `http://localhost:5000/test/?HOST_PORT=ws://127.0.0.1:[port]`.

Remember to run `npm run build` before release commit.

## Contributon

Please use the `.prettierrc` at the root of the project along with [Prettier default settings](https://prettier.io/docs/en/options.html) to format your code.

## Annotations

- [ngld/OverlayPlugin](https://github.com/ngld/OverlayPlugin) - MIT License
- [hibiyasleep/OverlayPlugin](https://github.com/hibiyasleep/OverlayPlugin) - MIT License
- [RainbowMage/OverlayPlugin](https://github.com/RainbowMage/OverlayPlugin) - MIT License

> Copyright © 2020-present DSRKafuU (<https://dsrkafuu.su>)
