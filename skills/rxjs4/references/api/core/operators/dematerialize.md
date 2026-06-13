### `Rx.Observable.prototype.dematerialize()`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/dematerialize.js "View in source")

Dematerializes the explicit notification values of an observable sequence as implicit notifications.

#### Returns
*(`Observable`)*: An observable sequence exhibiting the behavior corresponding to the source sequence's notification values.

#### Example
```js
var source = Rx.Observable
  .from([
    Rx.Notification.createOnNext(42),
    Rx.Notification.createOnError(new Error('woops'))
  ])
  .dematerialize();

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
// => Error: Error: woops
```
