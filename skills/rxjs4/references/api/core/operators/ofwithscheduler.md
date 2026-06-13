### `Rx.Observable.ofWithScheduler([scheduler], ...args)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/of.js "View in source")

Converts arguments to an observable sequence, using an optional scheduler to enumerate the arguments.

#### Arguments
1. `[scheduler]` *(Scheduler)*: An optional scheduler used to enumerate the arguments.
2. `args` *(Arguments)*: A list of arguments to turn into an Observable sequence.

#### Returns
*(`Observable`)*: The observable sequence whose elements are pulled from the given arguments.

#### Example
```js
var source = Rx.Observable.ofWithScheduler(Rx.Scheduler.timeout, 1,2,3);

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

// => Next: 1
// => Next: 2
// => Next: 3
// => Completed
```
