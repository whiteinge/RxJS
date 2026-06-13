### `Rx.Observable.prototype.skipUntil(other)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/skipuntil.js "View in source")

Returns the values from the source observable sequence only after the other observable sequence produces a value.

#### Arguments
1. `other` *(`Observable` | `Promise`)*: The observable sequence or Promise that triggers propagation of elements of the source sequence.

#### Returns
*(`Observable`)*: An observable sequence containing the elements of the source sequence starting from the point the other sequence triggered propagation.

#### Example
```js
var source = Rx.Observable.timer(0, 1000)
    .skipUntil(Rx.Observable.timer(5000));

var subscription = source.subscribe(
    function (x) {
        console.log('Next: ' + x);
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Next: 6
// => Next: 7
// => Next: 8
// => Completed
```
