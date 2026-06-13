### `Rx.Observable.prototype.doOnCompleted(onCompleted, [thisArg])`
### `Rx.Observable.prototype.tapOnCompleted(onCompleted, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/tap.js "View in source")

Invokes an action upon graceful termination of the observable sequence.

This method can be used for debugging, logging, etc. of query behavior by intercepting the message stream to run arbitrary actions for messages on the pipeline.

#### Arguments
1. `oncompleted` *(`Function`)*: Function to invoke upon graceful termination of the observable sequence.
2. [`thisArg`] *(Any)*: Object to use as this when executing callback.

#### Returns
*(`Observable`)*: The source sequence with the side-effecting behavior applied.

#### Example
```js
/* Using a function */
var source = Rx.Observable.range(0, 3)
  .doOnCompleted(
    function () { console.log('Do Completed'); }
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

// => Next: 0
// => Next: 1
// => Next: 2
// => Do Completed
// => Completed

/* Using a thisArg */

var source = Rx.Observable.range(0, 3)
  .doOnCompleted(
    function () { this.log('Do Completed'); },
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

// => Next: 0
// => Next: 1
// => Next: 2
// => Do Completed
// => Completed
```
