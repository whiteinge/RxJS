### `Rx.Observable.prototype.zipIterable(...args, [resultSelector])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/zipiterable.js "View in source")

Merges the current observable sequence with iterables such as `Map`, `Array`, `Set` into one observable sequence by using the selector function whenever all of the observable sequences or an array have produced an element at a corresponding index.

#### Arguments
1. `args` *(`Arguments`)*: Arguments of Arrays, Maps, Sets or other iterables.
2. `[resultSelector]` *(Function)*: A function which takes the inputs at the specified index and combines them together.  If omitted, a list with the elements of the observable sequences at corresponding indexes will be yielded.

#### Returns
*(`Observable`)*: An observable sequence containing the result of combining elements of the sources using the specified result selector function.  If omitted, a list with the elements of the observable sequences at corresponding indexes will be yielded.

#### Example
```js
var array = [3, 4, 5];

var source = Rx.Observable.range(0, 3)
  .zipIterable(
    array,
    function (s1, s2) { return s1 + ':' + s2; }
  );

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

// => Next: 0:3
// => Next: 1:4
// => Next: 2:5
// => Completed
```
