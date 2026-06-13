### `Rx.Observable.prototype.zip(...args, [resultSelector])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/zip.js "View in source")

Merges the specified observable sequences or Promises into one observable sequence by using the selector function whenever all of the observable sequences or an array have produced an element at a corresponding index.

#### Arguments
1. `args` *(`Arguments` | `Array`)*: Arguments or an array of observable sequences.
2. `[resultSelector]` *(Function)*: A function which takes the inputs at the specified index and combines them together.  If omitted, a list with the elements of the observable sequences at corresponding indexes will be yielded.

#### Returns
*(`Observable`)*: An observable sequence containing the result of combining elements of the sources using the specified result selector function.

#### Example
```js
/* Without a result selector */
var range = Rx.Observable.range(0, 5);

var source = range.zip(
  range.skip(1),
  range.skip(2)
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

// => Next: 0,1,2
// => Next: 1,2,3
// => Next: 2,3,4
// => Completed  

/* Using arguments */
var range = Rx.Observable.range(0, 5);

var source = range.zip(
  range.skip(1),
  range.skip(2),
  function (s1, s2, s3) {
    return s1 + ':' + s2 + ':' + s3;
  }
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

// => Next: 0:1:2
// => Next: 1:2:3
// => Next: 2:3:4
// => Completed
```
