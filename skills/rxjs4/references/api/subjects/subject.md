# `Rx.Subject` class #

Represents an object that is both an observable sequence as well as an observer. Each notification is broadcasted to all subscribed observers.

This class inherits both from the `Rx.Observable` and `Rx.Observer` classes.

## Usage ##

The following example shows the basic usage of an Rx.Subject.

```js
var subject = new Rx.Subject();

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

subject.onNext(42);

// => Next: 42

subject.onNext(56);

// => Next: 56

subject.onCompleted();

// => Completed
```
