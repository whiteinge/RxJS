### `Rx.Observable.spawn(fn)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/spawn.js "View in source")

Spawns a generator function which allows for Promises, Observable sequences, Arrays, Objects, Generators and functions.

#### Arguments
1. `fn` *(`Function`)*: The spawning function.

#### Returns
*(`Observable`)*: An Observable with the final result

#### Example
```js
var Rx = require('rx');

var spawned = Rx.Observable.spawn(function* () {
  var a = yield cb => cb(null, 'a');
  var b = yield ['b'];
  var c = yield Rx.Observable.just('c');
  var d = yield Rx.Observable.just('d');
  var e = yield Promise.resolve('e');
  return a + b + c + d + e;
});

spawned.subscribe(
  function (x) { console.log('next %s', x); },
  function (e) { console.log('error %s', e); },
  function () { console.log('completed'); }
);

// => next 'abcde'
// => completed
```
