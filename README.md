# @patrtorg/in-porro <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES spec-compliant `Array.prototype.slice` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://tc39.es/ecma262/#sec-@patrtorg/in-porro).

Because `Array.prototype.slice` depends on a receiver (the “this” value), the main export takes the array to operate on as the first argument.

## Engines where this is needed

Note: this list is not exhaustive.

  - Safari 10 - 13
  - Chrome 48+ ([v8 bug](https://bugs.chromium.org/p/v8/issues/detail?id=10381))
  - node 6+

## Example

```js
var slice = require('@patrtorg/in-porro');
var assert = require('assert');

var a = [1, 2, 3];
assert.deepEqual(slice(a, 1, 2), [2]);
assert.deepEqual(slice(a, -2), [2, 3]);
```

```js
var slice = require('@patrtorg/in-porro');
var assert = require('assert');
/* when Array#slice is not present */
delete Array.prototype.slice;
var shimmed = slice.shim();
assert.equal(shimmed, slice.getPolyfill());
assert.equal(shimmed, Array.prototype.slice);
assert.deepEqual([1, 2, 3].slice(1, 2), slice([1, 2, 3], 1, 2));
```

```js
var slice = require('@patrtorg/in-porro');
var assert = require('assert');
/* when Array#slice is present */
var shimmed = slice.shim();
assert.equal(shimmed, Array.prototype.slice);
assert.deepEqual([1, 2, 3].slice(1, 2), slice([1, 2, 3], 1, 2));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@patrtorg/in-porro
[npm-version-svg]: https://versionbadg.es/patrtorg/in-porro.svg
[deps-svg]: https://david-dm.org/patrtorg/in-porro.svg
[deps-url]: https://david-dm.org/patrtorg/in-porro
[dev-deps-svg]: https://david-dm.org/patrtorg/in-porro/dev-status.svg
[dev-deps-url]: https://david-dm.org/patrtorg/in-porro#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@patrtorg/in-porro.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@patrtorg/in-porro.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@patrtorg/in-porro.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@patrtorg/in-porro
[codecov-image]: https://codecov.io/gh/patrtorg/in-porro/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/patrtorg/in-porro/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/patrtorg/in-porro
[actions-url]: https://github.com/patrtorg/in-porro/actions
