### `Rx.Observable.prototype.doOnError(onError, [thisArg])`
### `Rx.Observable.prototype.tapOnError(onError, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/tap.js "View in source")

Invokes an action upon exceptional termination of the observable sequence.

This method can be used for debugging, logging, etc. of query behavior by intercepting the message stream to run arbitrary actions for messages on the pipeline.

#### Arguments
1. `onError` *(`Function`)*: Function to invoke upon exceptional termination of the observable sequence.
2. [`thisArg`] *(Any)*: Object to use as this when executing callback.

#### Returns
*(`Observable`)*: The source sequence with the side-effecting behavior applied.

#### Example
```js
/* Using a function */
var source = Rx.Observable.throw(new Error())
  .doOnError(
    function (err) { console.log('Do Error: %s', err); }
  );

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

// => Do Error: Error
// => Error: Error

/* Using a thisArg */

var source = Rx.Observable.throw(new Error())
  .doOnError(
    function (err) { this.log('Do Error: %s', err); },
    console
  );

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

// => Do Error: Error
// => Error: Error
```
