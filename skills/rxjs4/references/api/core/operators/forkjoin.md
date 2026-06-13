### `Rx.Observable.forkJoin(...args, [resultSelector])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/tests/observable/forkjoin.js "View in source")

Runs all observable sequences in parallel and collect their last elements.

#### Arguments
1. `args` *(Arguments | Array)*: An array or arguments of Observable sequences or Promises to collect the last elements for.
2. `resultSelector`: `Function` - The result selector from all the values produced. If not specified, `forkJoin` will return the results as an array.

#### Returns
*(`Observable`)*: An observable sequence with an array collecting the last elements of all the input sequences or the result of the result selector if specified.

#### Example
```js
/* Without a selector */
var source = Rx.Observable.forkJoin(
  Rx.Observable.return(42),
  Rx.Observable.range(0, 10),
  Rx.Observable.from([1,2,3]),
  RSVP.Promise.resolve(56)
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

// => Next: [42, 9, 3, 56]
// => Completed

var source = Rx.Observable.forkJoin(
  Rx.Observable.just(42),
  Rx.Observable.just(56),
  function (x, y) { return x + y; }
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

// => Next: 98
// => Completed
```
