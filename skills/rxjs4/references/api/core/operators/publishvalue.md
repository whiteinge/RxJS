### `Rx.Observable.prototype.publishValue([selector], initialValue)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/publishvalue.js "View in source")

Returns an observable sequence that is the result of invoking the selector on a connectable observable sequence that shares a single subscription to the underlying sequence and starts with initialValue.

This operator is a specialization of `multicast` using a `Rx.BehaviorSubject`.

#### Arguments
1. `[selector]`: `Function` - Selector function which can use the multicasted source sequence as many times as needed, without causing multiple subscriptions to the source sequence. Subscribers to the given source will immediately receive the initial value, followed by all notifications of the source from the time of the subscription on.
2. `initialValue`: `Any` - Initial value received by observers upon subscription.

#### Returns
`ConnectableObservable` - An observable sequence that contains the elements of a sequence produced by multicasting the source sequence within a selector function and initial value.

#### Example
```js
var interval = Rx.Observable.interval(1000);

var source = interval
  .take(2)
  .tap(function (x) {
    console.log('Side effect');
  });

var published = source.publishValue(42);

published.subscribe(createObserver('SourceA'));
published.subscribe(createObserver('SourceB'));

var connection = published.connect();

function createObserver(tag) {
  return Rx.Observer.create(
    function (x) {
      console.log('Next: ' + tag + x);
    },
    function (err) {
      console.log('Error: ' + err);
    },
    function () {
      console.log('Completed');
    });
}

// => Next: SourceA42
// => Next: SourceB42
// => Side effect
// => Next: SourceA0
// => Next: SourceB0
// => Side effect
// => Next: SourceA1
// => Next: SourceB1
// => Completed
// => Completed
```
