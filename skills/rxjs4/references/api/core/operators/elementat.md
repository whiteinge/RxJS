### `Rx.Observable.prototype.elementAt(index, [defaultValue])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/elementat.js "View in source")

Returns the element at a specified index in a sequence.  If the specified index is out of bounds and no default value was given `onError` will be called with an error, however, if a default value has been specified, that value will be returned via an `onNext` call.

#### Arguments
1. `index` *(`Number`)*: The zero-based index of the element to retrieve.
2. `[defaultValue]` *(`Any`)*: Default value if no such element exists.

#### Returns
*(`Observable`)*: An observable sequence that produces the element at the specified position in the source sequence. If the specified index is out of bounds and no default value was given `onError` will be called with an error, however, if a default value has been specified, that value will be returned via an `onNext` call.

#### Example
```js
/* Finds an index */
var source = Rx.Observable.from([1,2,3,4])
    .elementAt(1);

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

// => Next: 2
// => Completed

/* With default value */
var source = Rx.Observable.from([1,2,3,4])
  .elementAt(4, 42);

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

// => Next: 42
// => Completed
```
