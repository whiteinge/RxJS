### `Rx.Observable.prototype.repeat(repeatCount)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/repeatproto.js "View in source")

Repeats the observable sequence a specified number of times. If the repeat count is not specified, the sequence repeats indefinitely.

#### Arguments
1. `repeatCount` *(`Number`)*:  Number of times to repeat the sequence. If not provided, repeats the sequence indefinitely.

#### Returns
*(`Observable`)*: The observable sequence producing the elements of the given sequence repeatedly.

#### Example
```js
var source = Rx.Observable.range(1, 3)
    .repeat(2);

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
// => Next: 1
// => Next: 2
// => Next: 3
// => Completed
```
