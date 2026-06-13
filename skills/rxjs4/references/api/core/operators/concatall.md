### `Rx.Observable.prototype.concatAll()` ###
### `Rx.Observable.prototype.concatObservable()` **DEPRECATED** ###
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/concatall.js "View in source")

Concatenates a sequence of observable sequences or promises into a single observable sequence.

#### Returns
*(`Observable`)*: The observable sequence that merges the elements of the inner sequences.

#### Example
```js
var source = Rx.Observable.range(0, 3)
  .map(function (x) { return Rx.Observable.range(x, 3); })
  .concatAll();

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

// => Next: 0
// => Next: 1
// => Next: 2
// => Next: 1
// => Next: 2
// => Next: 3
// => Next: 2
// => Next: 3
// => Next: 4
// => Completed
```
