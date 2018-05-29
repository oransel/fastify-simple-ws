# fastify-simple-ws

[![Build Status](https://travis-ci.org/gj/fastify-ws.svg?branch=master)](https://travis-ci.org/gj/fastify-ws) [![npm version](https://badge.fury.io/js/fastify-ws.svg)](https://www.npmjs.com/package/fastify-ws)

WebSocket support for [Fastify](https://github.com/fastify/fastify) built on the blazing fast [ws](http://npm.im/ws) library (removed  [uws](http://npm.im/uws) support).

## Example

In `server.js`:

```js
'use strict'

const fastify = require('fastify')()

fastify.register(require('fastify-ws'))

fastify.ready(err => {
  if (err) throw err

  console.log('Server started.')

  fastify.ws
    .on('connection', socket => {
      console.log('Client connected.')

      socket.on('message', msg => socket.send(msg)) // Creates an echo server

      socket.on('close', () => console.log('Client disconnected.'))
    })
})

fastify.listen(34567)
```

Then run `node server.js` and navigate to `http://localhost:34567` in your browser. In the browser's JavaScript console, open a client-side WebSocket connection:

```js
const host = location.origin.replace(/^http/, 'ws')
const ws = new WebSocket(host)
ws.onmessage = msg => console.log(msg.data)
```

Then, still in the browser console, send some messages to the server and watch as they're echoed back to you:

```js
ws.send('WebSockets are awesome!')
// => undefined
// LOG: WebSockets are awesome!
```

## Notes

This forked version removes the support for `uws`.

## License

Licensed under [MIT](./LICENSE).
