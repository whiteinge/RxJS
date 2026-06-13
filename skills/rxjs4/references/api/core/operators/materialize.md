### `Rx.Observable.prototype.materialize()`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/materialize.js "View in source")

Materializes the implicit notifications of an observable sequence as explicit notification values.

#### Returns
*(`Observable<Notification>`)*: An observable sequence containing the materialized notification values from the source sequence.

#### Example
```js
var source = Rx.Observable.of(1,2,3).materialize();

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

// => Next OnNext(1)
// => Next OnNext(2)
// => Next OnNext(3)
// => Next OnCompleted()
// => Completed
```
