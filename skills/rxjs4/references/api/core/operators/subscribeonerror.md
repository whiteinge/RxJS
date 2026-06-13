### `Rx.Observable.prototype.subscribeOnError(onError, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/observable.js "View in source")

Subscribes a function to invoke upon exceptional termination of the observable sequence.

#### Arguments
1. `onError` *(`Function`)*: Function to invoke upon exceptional termination of the observable sequence.
2. `[thisArg]` *(`Any`)*: Object to use as this when executing callback.

#### Returns
*(Disposable)*: The source sequence whose subscriptions and unsubscriptions happen on the specified scheduler.

#### Example
```js
/* Using functions */
var source = Rx.Observable.throw(new Error());

var subscription = source.subscribeOnError(
  function (err) {
    console.log('Error: %s', err);
  });

// => Error: Error

/* With a thisArg */
var source = Rx.Observable.throw(new Error());

var subscription = source.subscribeOnError(
  function (err) {
    this.log('Error: %s', err);
  }, console);

// => Error: Error
```
