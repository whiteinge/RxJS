### `Rx.Observable.prototype.some([predicate], [thisArg])` ###
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/some.js "View in source")

Determines whether any element of an observable sequence satisfies a condition if present, else if any items are in the sequence.

#### Arguments
1. `predicate` *(`Function`)*: A function to test each element for a condition.
2. `[thisArg]` *(`Any`)*: Object to use as this when executing callback.

#### Returns
*(`Observable`)*: An observable sequence containing a single element determining whether one of the elements in the source sequence pass the test in the specified predicate.

#### Example
```js
var source = Rx.Observable.of(1,2,3,4,5)
  .some(function (x) { return x % 2 === 0; });

var subscription = source.subscribe(
  function (x) {
    console.log('Next: %s', x);
  },
  function (err) {
    console.log('Error: %s', err);
  },
  function () {
    console.log('Completed');
  });

// => Next: true
// => Completed
```
