# typed-array-byte-offset <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Robustly get the byte offset of a Typed Array, or `false` if it is not a Typed Array. Works cross-realm, in every engine, even if the `byteOffset` property is overridden.

## Example

```js
var typedArrayByteOffset = require('typed-array-byte-offset');
var assert = require('assert');

assert.equal(false, typedArrayByteOffset(undefined));
assert.equal(false, typedArrayByteOffset(null));
assert.equal(false, typedArrayByteOffset(false));
assert.equal(false, typedArrayByteOffset(true));
assert.equal(false, typedArrayByteOffset([]));
assert.equal(false, typedArrayByteOffset({}));
assert.equal(false, typedArrayByteOffset(/a/g));
assert.equal(false, typedArrayByteOffset(new RegExp('a', 'g')));
assert.equal(false, typedArrayByteOffset(new Date()));
assert.equal(false, typedArrayByteOffset(42));
assert.equal(false, typedArrayByteOffset(NaN));
assert.equal(false, typedArrayByteOffset(Infinity));
assert.equal(false, typedArrayByteOffset(new Number(42)));
assert.equal(false, typedArrayByteOffset('foo'));
assert.equal(false, typedArrayByteOffset(Object('foo')));
assert.equal(false, typedArrayByteOffset(function () {}));
assert.equal(false, typedArrayByteOffset(function* () {}));
assert.equal(false, typedArrayByteOffset(x => x * x));
assert.equal(false, typedArrayByteOffset([]));

const buffer = new ArrayBuffer(32);

assert.equal(8, typedArrayByteOffset(new Int8Array(buffer, 8)));
assert.equal(8, typedArrayByteOffset(new Uint8Array(buffer, 8)));
assert.equal(8, typedArrayByteOffset(new Uint8ClampedArray(buffer, 8)));
assert.equal(4, typedArrayByteOffset(new Int16Array(buffer, 4)));
assert.equal(4, typedArrayByteOffset(new Uint16Array(buffer, 4)));
assert.equal(8, typedArrayByteOffset(new Int32Array(buffer, 8)));
assert.equal(8, typedArrayByteOffset(new Uint32Array(buffer, 8)));
assert.equal(16, typedArrayByteOffset(new Float32Array(buffer, 16)));
assert.equal(16, typedArrayByteOffset(new Float64Array(buffer, 16)));
assert.equal(16, typedArrayByteOffset(new BigInt64Array(buffer, 16)));
assert.equal(16, typedArrayByteOffset(new BigUint64Array(buffer, 16)));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/typed-array-byte-offset
[npm-version-svg]: https://versionbadg.es/inspect-js/typed-array-byte-offset.svg
[deps-svg]: https://david-dm.org/inspect-js/typed-array-byte-offset.svg
[deps-url]: https://david-dm.org/inspect-js/typed-array-byte-offset
[dev-deps-svg]: https://david-dm.org/inspect-js/typed-array-byte-offset/dev-status.svg
[dev-deps-url]: https://david-dm.org/inspect-js/typed-array-byte-offset#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/typed-array-byte-offset.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/typed-array-byte-offset.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/typed-array-byte-offset.svg
[downloads-url]: https://npm-stat.com/charts.html?package=typed-array-byte-offset
[codecov-image]: https://codecov.io/gh/inspect-js/typed-array-byte-offset/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/inspect-js/typed-array-byte-offset/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/inspect-js/typed-array-byte-offset
[actions-url]: https://github.com/inspect-js/typed-array-byte-offset/actions



# yocto-queue [![](https://badgen.net/bundlephobia/minzip/yocto-queue)](https://bundlephobia.com/result?p=yocto-queue)

> Tiny queue data structure

You should use this package instead of an array if you do a lot of `Array#push()` and `Array#shift()` on large arrays, since `Array#shift()` has [linear time complexity](https://medium.com/@ariel.salem1989/an-easy-to-use-guide-to-big-o-time-complexity-5dcf4be8a444#:~:text=O(N)%E2%80%94Linear%20Time) *O(n)* while `Queue#dequeue()` has [constant time complexity](https://medium.com/@ariel.salem1989/an-easy-to-use-guide-to-big-o-time-complexity-5dcf4be8a444#:~:text=O(1)%20%E2%80%94%20Constant%20Time) *O(1)*. That makes a huge difference for large arrays.

> A [queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)) is an ordered list of elements where an element is inserted at the end of the queue and is removed from the front of the queue. A queue works based on the first-in, first-out ([FIFO](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics))) principle.

## Install

```
$ npm install yocto-queue
```

## Usage

```js
const Queue = require('yocto-queue');

const queue = new Queue();

queue.enqueue('🦄');
queue.enqueue('🌈');

console.log(queue.size);
//=> 2

console.log(...queue);
//=> '🦄 🌈'

console.log(queue.dequeue());
//=> '🦄'

console.log(queue.dequeue());
//=> '🌈'
```

## API

### `queue = new Queue()`

The instance is an [`Iterable`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols), which means you can iterate over the queue front to back with a “for…of” loop, or use spreading to convert the queue to an array. Don't do this unless you really need to though, since it's slow.

#### `.enqueue(value)`

Add a value to the queue.

#### `.dequeue()`

Remove the next value in the queue.

Returns the removed value or `undefined` if the queue is empty.

#### `.clear()`

Clear the queue.

#### `.size`

The size of the queue.

## Related

- [quick-lru](https://github.com/sindresorhus/quick-lru) - Simple “Least Recently Used” (LRU) cache

