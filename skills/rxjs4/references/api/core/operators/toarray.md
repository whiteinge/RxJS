### `Rx.Observable.prototype.toArray()`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/toarray.js "View in source")

Creates a list from an observable sequence.

#### Returns
*(`Observable`)*: An observable sequence containing a single element with a list containing all the elements of the source sequence.

#### Example
```js
var source = Rx.Observable.timer(0, 1000)
    .take(5)
    .toArray();

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

// => Next: [0,1,2,3,4]
// => Completed
```
