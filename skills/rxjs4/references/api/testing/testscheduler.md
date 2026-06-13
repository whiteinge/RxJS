# `Rx.TestScheduler` class #

Virtual time scheduler used for testing applications and libraries built using Reactive Extensions.  This inherits from the `Rx.VirtualTimeScheduler` class.

## Usage ##

The following shows an example of using the `Rx.TestScheduler`.  In order to make the end comparisons work, you must implement a collection assert, for example here using QUnit.

```js
function createMessage(expected, actual) {
  return 'Expected: [' + expected.toString() + ']\r\nActual: [' + actual.toString() + ']';
}

// Using QUnit testing for assertions
var collectionAssert = {
  assertEqual: function (actual, expected) {
    var comparer = Rx.internals.isEqual, isOk = true;

    if (expected.length !== actual.length) {
      ok(false, 'Not equal length. Expected: ' + expected.length + ' Actual: ' + actual.length);
      return;
    }

    for(var i = 0, len = expected.length; i < len; i++) {
      isOk = comparer(expected[i], actual[i]);
      if (!isOk) {
        break;
      }
    }

    ok(isOk, createMessage(expected, actual));
  }
};

var onNext = Rx.ReactiveTest.onNext,
  onCompleted = Rx.ReactiveTest.onCompleted,
  subscribe = Rx.ReactiveTest.subscribe;

var scheduler = new Rx.TestScheduler();

// Create hot observable which will start firing
var xs = scheduler.createHotObservable(
  onNext(150, 1),
  onNext(210, 2),
  onNext(220, 3),
  onCompleted(230)
);

// Note we'll start at 200 for subscribe, hence missing the 150 mark
var res = scheduler.startScheduler(function () {
  return xs.map(function (x) { return x * x });
});

// Implement collection assertion
collectionAssert.assertEqual(res.messages, [
  onNext(210, 4),
  onNext(220, 9),
  onCompleted(230)
]);

// Check for subscribe/unsubscribe
collectionAssert.assertEqual(xs.subscriptions, [
  subscribe(200, 230)
]);
```
