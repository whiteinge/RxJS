### `Rx.Observable.prototype.find(predicate, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/find.js)
Searches for an element that matches the conditions defined by the specified predicate, and returns the first occurrence within the entire Observable sequence.

#### Arguments
1. `predicate` *(`Function`)*: A function to test each source element for a condition;  The callback is called with the following information:
    1. the value of the element
    2. the index of the element
    3. the Observable object being subscribed
2. `[thisArg]` *(`Any`)*: Object to use as `this` when executing the predicate.

#### Returns
*(`Observable`)*: An Observable sequence with the first element that matches the conditions defined by the specified predicate, if found; otherwise, an empty sequence.

#### Example
```js
/* Found an element */
var array = [1,2,3,4];

var source = Rx.Observable.from(array)
  .find(function (x, i, obs) { return x === 1; });

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

// => Next: 1
// => Completed

/* Not found */
var array = [1,2,3,4];

var source = Rx.Observable.from(array)
  .find(function (x, i, obs) { return x === 5; });

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

// => Completed
```
