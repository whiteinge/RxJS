### `Rx.Observable.prototype.thenDo(selector)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/thendo.js "View in source")

Matches when the observable sequence has an available value and projects the value.

#### Arguments
1. `selector` *(`Function`)*: Selector that will be invoked for values in the source sequence.

#### Returns
*(`Plan`)*: Plan that produces the projected values, to be fed (with other plans) to the when operator.

#### Example
```js
var selector = function (x, y) { return x + ", " + y; };

var source = Rx.Observable.when(
    Rx.Observable.interval(250).and(Rx.Observable.of("A", "B", "C")).thenDo(selector),
    Rx.Observable.interval(300).and(Rx.Observable.of("a", "b")).thenDo(selector)
);

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

// => Next: 0, A 
// => Next: 0, a
// => Next: 1, B
// => Next: 1, b
// => Next: 2, C
// => Completed
```
