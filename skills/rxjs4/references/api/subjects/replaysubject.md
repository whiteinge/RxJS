# `Rx.ReplaySubject` class #

Represents an object that is both an observable sequence as well as an observer.  Each notification is broadcasted to all subscribed and future observers, subject to buffer trimming policies.

This class inherits both from the `Rx.Observable` and `Rx.Observer` classes.

## Usage ##

The follow example shows the basic usage of an `Rx.ReplaySubject` class.  Note that this only holds the past two items in the cache.

```js
var subject = new Rx.ReplaySubject(2 /* buffer size */);

subject.onNext('a');
subject.onNext('b');
subject.onNext('c');

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

// => Next: b
// => Next: c

subject.onNext('d');
// => Next: d
```
