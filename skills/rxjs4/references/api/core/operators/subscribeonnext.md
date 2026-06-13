### `Rx.Observable.prototype.subscribeOnNext(onNext, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/observable.js "View in source")

Subscribes a function to invoke for each element in the observable sequence.

#### Arguments
1. `onNext` *(`Function`)*: Function to invoke for each element in the observable sequence.
2. `[thisArg]` *(`Any`)*: Object to use as this when executing callback.

#### Returns
*(Disposable)*: The source sequence whose subscriptions and unsubscriptions happen on the specified scheduler.

#### Example
```js
/* Using functions */
var source = Rx.Observable.range(0, 3)

var subscription = source.subscribeOnNext(
  function (x) {
    console.log('Next: %s', x);
  });

// => Next: 0
// => Next: 1
// => Next: 2

/* With a thisArg */
var source = Rx.Observable.range(0, 3)

var subscription = source.subscribeOnNext(
  function (x) {
    this.log('Next: %s', x);
  }, console);

// => Next: 0
// => Next: 1
// => Next: 2
```
