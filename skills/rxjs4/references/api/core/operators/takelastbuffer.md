### `Rx.Observable.prototype.takeLastBuffer(count)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/takelastbuffer.js "View in source")

Returns an array with the specified number of contiguous elements from the end of an observable sequence.

#### Arguments
1. `count` *(`Number`)*: Number of elements to bypass at the end of the source sequence.

#### Returns
*(`Observable`)*: An observable sequence containing a single array with the specified number of elements from the end of the source sequence.

#### Example
```js
var source = Rx.Observable.range(0, 5)
    .takeLastBuffer(3);

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

// => Next: 2,3,4
// => Completed
```
