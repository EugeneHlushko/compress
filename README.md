# Koa Compress [![Build Status](https://travis-ci.org/koajs/compress.svg?branch=master)](https://travis-ci.org/koajs/compress)

Compress middleware for Koa

Install `v1.x` for Koa v1. Install `v2.x` or `next` for Koa v2.

## Example

```js
var compress = require('koa-compress')
var koa = require('koa')

var app = koa()
app.use(compress({
  filter: function (content_type) {
  	return /text/i.test(content_type)
  },
  threshold: 2048,
  flush: require('zlib').Z_SYNC_FLUSH
}))
```

## Options

The options are passed to `zlib`: http://nodejs.org/api/zlib.html#zlib_options

### filter

An optional function that checks the response content type to decide whether to compress.
By default, it uses [compressible](https://github.com/expressjs/compressible).

### threshold

Minimum response size in bytes to compress.
Default `1024` bytes or `1kb`.

## Manually turning compression on and off

You can always enable compression by setting `this.compress = true`.
You can always disable compression by setting `this.compress = false`.
This bypasses the filter check.

```js
app.use(function (next) {
  return function *() {
    this.compress = true
    this.body = fs.createReadStream(file)
  }
})
```
