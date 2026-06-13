### `Rx.Observable.prototype.subscribeOnCompleted(onCompleted, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/observable.js "View in source")

Subscribes a function to invoke upon graceful termination of the observable sequence.

#### Arguments
1. `onCompleted` *(`Function`)*: Function to invoke upon graceful termination of the observable sequence.
2. `[thisArg]` *(`Any`)*: Object to use as this when executing callback.

#### Returns
*(Disposable)*: The source sequence whose subscriptions and unsubscriptions happen on the specified scheduler.

#### Example
```js
/* Using functions */
var source = Rx.Observable.range(0, 3);

var subscription = source.subscribeOnCompleted(
  function () {
    console.log('Completed');
  });

// => Completed

/* With a thisArg */
var source = Rx.Observable.range(0, 3);

var subscription = source.subscribeOnCompleted(
  function (err) {
    this.log('Completed');
  }, console);

// => Completed
```
