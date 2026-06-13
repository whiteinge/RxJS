### `Rx.Observable.wrap(fn)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/spawn.js "View in source")

Wrap the given generator `fn` into a function that returns an Observable.

#### Arguments
1. `fn` *(`Function`)*: A generator function to wrap.

#### Returns
*(`Function`)*: A function once executed, returns an Observable.

#### Example
```js
var Rx = require('rx');

var fn = Rx.Observable.wrap(function* (val) {
  return yield Rx.Observable.just(val);
});

fn(42).subscribe(
  function (x) { console.log('next %s', x); },
  function (e) { console.log('error %s', e); },
  function () { console.log('completed'); }
);

// => next 42
// => completed
```
