# `Rx.BehaviorSubject` class #

Represents a value that changes over time.  Observers can subscribe to the subject to receive the last (or initial) value and all subsequent notifications. If you are looking for BehaviorSubject without initial value see [`Rx.ReplaySubject`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/subjects/replaysubject.md).

This class inherits both from the `Rx.Observable` and `Rx.Observer` classes.

## Usage ##

The follow example shows the basic usage of an `Rx.BehaviorSubject` class.

```js
/* Initialize with initial value of 42 */
var subject = new Rx.BehaviorSubject(42);

var subscription = subject.subscribe(
    function (x) {
        console.log('Next: ' + x.toString());
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Next: 42

subject.onNext(56);
// => Next: 56

subject.onCompleted();
// => Completed
```
