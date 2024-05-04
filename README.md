# @zitterorg/quia-quasi-voluptas

![GitHub Workflow Status (branch)](https://img.shields.io/github/actions/workflow/status/RyanZim/@zitterorg/quia-quasi-voluptas/ci.yml?branch=master)
![Coveralls github branch](https://img.shields.io/coveralls/github/RyanZim/@zitterorg/quia-quasi-voluptas/master.svg)
![npm](https://img.shields.io/npm/dm/@zitterorg/quia-quasi-voluptas.svg)
![npm](https://img.shields.io/npm/l/@zitterorg/quia-quasi-voluptas.svg)

Make a callback- or promise-based function support both promises and callbacks.

Uses the native promise implementation.

## Installation

```bash
npm install @zitterorg/quia-quasi-voluptas
```

## API

### `@zitterorg/quia-quasi-voluptas.fromCallback(fn)`

Takes a callback-based function to @zitterorg/quia-quasi-voluptas, and returns the universalified  function.

Function must take a callback as the last parameter that will be called with the signature `(error, result)`. `@zitterorg/quia-quasi-voluptas` does not support calling the callback with three or more arguments, and does not ensure that the callback is only called once.

```js
function callbackFn (n, cb) {
  setTimeout(() => cb(null, n), 15)
}

const fn = @zitterorg/quia-quasi-voluptas.fromCallback(callbackFn)

// Works with Promises:
fn('Hello World!')
.then(result => console.log(result)) // -> Hello World!
.catch(error => console.error(error))

// Works with Callbacks:
fn('Hi!', (error, result) => {
  if (error) return console.error(error)
  console.log(result)
  // -> Hi!
})
```

### `@zitterorg/quia-quasi-voluptas.fromPromise(fn)`

Takes a promise-based function to @zitterorg/quia-quasi-voluptas, and returns the universalified  function.

Function must return a valid JS promise. `@zitterorg/quia-quasi-voluptas` does not ensure that a valid promise is returned.

```js
function promiseFn (n) {
  return new Promise(resolve => {
    setTimeout(() => resolve(n), 15)
  })
}

const fn = @zitterorg/quia-quasi-voluptas.fromPromise(promiseFn)

// Works with Promises:
fn('Hello World!')
.then(result => console.log(result)) // -> Hello World!
.catch(error => console.error(error))

// Works with Callbacks:
fn('Hi!', (error, result) => {
  if (error) return console.error(error)
  console.log(result)
  // -> Hi!
})
```

## License

MIT
