# `Rx.AsyncSubject` class #

Represents the result of an asynchronous operation.  The last value before the OnCompleted notification, or the error received through OnError, is sent to all subscribed observers.

This class inherits both from the `Rx.Observable` and `Rx.Observer` classes.

## Usage ##

The following example shows caching on the last value produced when followed by an onCompleted notification which makes it available to all subscribers.

```js
var subject = new Rx.AsyncSubject();

var i = 0;
var handle = setInterval(function () {
	subject.onNext(i);
	if (++i > 3) {
		subject.onCompleted();
		clearInterval(handle);
	}
}, 500);

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

// => Next: 3
// => Completed
```
