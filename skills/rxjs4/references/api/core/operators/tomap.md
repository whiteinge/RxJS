### `Rx.Observable.prototype.toMap(keySelector, [elementSelector])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/tomap.js "View in source")

Converts the observable sequence to a Map if it exists.  Note that this only works in an ES6 environment or polyfilled.

#### Arguments
1. `keySelector` *(`Function`)*: A function which produces the key for the Map.
2. `[elementSelector]` *(`Function`)*: An optional function which produces the element for the Map. If not present, defaults to the value from the observable sequence.

#### Returns
*(`Observable`)*: An observable sequence with a single value of a Map containing the values from the observable sequence.

#### Example
```js
var source = Rx.Observable.timer(0, 1000)
    .take(5)
    .toMap(function (x) { return x * 2; }, function (x) { return x * 4; });

var subscription = source.subscribe(
    function (x) {
        var arr = [];
        x.forEach(function (value, key) { arr.push(value, key); })
        console.log('Next: ' + arr);
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Next: [0,0,2,4,4,8,6,12,8,16]
// => Completed
```
