### `Rx.Observable.fromPromise(promise)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/frompromise.js "View in source")

Converts a Promises/A+ spec compliant Promise and/or ES2015 compliant Promise or a factory function which returns said Promise to an Observable sequence.

#### Arguments
1. `promise|Function`: `Promise` - Promises/A+ spec compliant Promise to an Observable sequence or a function which returns a Promise.

#### Returns
`Observable`: An Observable sequence which wraps the existing promise success and failure.

#### Example
```js
// Create a factory function which returns a promise
var promiseFn = function () { return Promise.resolve(42); };

var source = Rx.Observable.fromPromise(promiseFn);

var subscription = source.subscribe(
  function (x) {
    console.log('Next: %s', x);
  },
  function (err) {
    console.log('Error: %s', err);
  },
  function () {
    console.log('Completed');
  });

// Create a promise which resolves 42
var promise1 = Promise.resolve(42)

var source1 = Rx.Observable.fromPromise(promise1);

var subscription1 = source1.subscribe(
  function (x) {
    console.log('Next: %s', x);
  },
  function (err) {
    console.log('Error: %s', err);
  },
  function () {
    console.log('Completed');
  });

// => Next: 42
// => Completed

// Create a promise which rejects with an error
var promise2 = Promise.reject(new Error('reason'));

var source2 = Rx.Observable.fromPromise(promise2);

var subscription2 = source2.subscribe(
  function (x) {
    console.log('Next: %s', x);
  },
  function (err) {
    console.log('Error: %s', err);
  },
  function () {
    console.log('Completed');
  });

// => Error: Error: reject
```
