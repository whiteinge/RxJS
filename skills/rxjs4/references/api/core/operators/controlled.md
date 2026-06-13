### `Rx.Observable.prototype.controlled([enableQueue])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/backpressure/controlled.js "View in source")

Attaches a controller to the observable sequence with the ability to queue.

#### Arguments
1. `[enableQueue]` *(Boolean)*: Whether to enable queueing.  If not specified, defaults to true.

#### Returns
*(`Observable`)*: An observable sequence which can be used to request values from the sequence.

#### Example
```js
var source = Rx.Observable.range(0, 10).controlled();

var subscription = source.subscribe(
    function (x) {
        console.log('Next: ' + x.toString());
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

source.request(2);

// => Next: 0
// => Next: 1
```
