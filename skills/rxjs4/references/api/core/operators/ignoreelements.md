### `Rx.Observable.prototype.ignoreElements()`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/ignoreelements.js "View in source")

Ignores all elements in an observable sequence leaving only the termination messages.

#### Returns
*(`Observable`)*: An empty observable sequence that signals termination, successful or exceptional, of the source sequence.

#### Example
```js
var source = Rx.Observable.range(0, 10)
    .ignoreElements();

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

// => Completed
```
