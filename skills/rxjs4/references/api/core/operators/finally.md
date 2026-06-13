### `Rx.Observable.prototype.finally(action)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/finally.js "View in source")

Invokes a specified action after the source observable sequence terminates gracefully or exceptionally.  There is an alias called `finallyAction` for browsers <IE9

#### Arguments
1. `action` *(`Function`)*: A function to invoke after the source observable sequence terminates.

#### Returns
*(`Observable`)*: The source sequence with the side-effecting behavior applied.

#### Example
```js
/* Terminated by error still fires function */
var source = Rx.Observable.throw(new Error())
  .finally(function () { console.log('Finally'); });

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

// => Error: Error
// => Finally
```
