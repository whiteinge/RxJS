### `Rx.Observable.prototype.last([predicate], [thisArg])`
### `Rx.Observable.prototype.last([settings])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/last.js "View in source")

Returns the last element of an observable sequence that satisfies the condition in the predicate if specified, else the last element.  If no element was found and no default value is specified, `onError` is called with an error, however if a default value was specified, it will be yielded via an `onNext` call.

#### Arguments
`Rx.Observable.prototype.last([predicate], [thisArg], [defaultValue])`

1. `[predicate]` *(`Function`)*: A predicate function to evaluate for elements in the source sequence. The callback is called with the following information:
    1. the value of the element
    2. the index of the element
    3. the Observable object being subscribed
2. `[thisArg]` *(`Any`)*: Object to use as `this` when executing the predicate.
3. `[defaultValue]` *(`Any`)*: Default value if no such element exists.

`Rx.Observable.prototype.last([settings])`

1. `[settings]` *(`Object`)*: An object with the following fields
    - `[predicate]` *(`Function`)*: A predicate function to evaluate for elements in the source sequence. The callback is called with the following information:
        1. the value of the element
        2. the index of the element
        3. the Observable object being subscribed
    - `[thisArg]` *(`Any`)*: Object to use as `this` when executing the predicate.
    - `[defaultValue]` *(`Any`)*: Default value if no such element exists.

#### Returns
*(`Observable`)*: Sequence containing the last element in the observable sequence that satisfies the condition.

#### Example
```js
/* Default value */
var source = Rx.Observable.empty().last({defaultValue: 42});

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

/* Without predicate */
var source = Rx.Observable.range(0, 10).last();

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

// => Next: 9
// => Completed

/* With predicate */
var source = Rx.Observable.range(0, 10)
  .last(function (x, idx, obs) {
    return x % 2 === 0;
  });

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

// => Next: 8
// => Completed
```
