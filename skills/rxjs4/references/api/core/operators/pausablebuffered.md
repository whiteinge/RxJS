### `Rx.Observable.prototype.pausableBuffered(pauser)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/backpressure/pausablebuffered.js "View in source")

Pauses the underlying observable sequence based upon the observable sequence which yields true/false, and yields the values that were buffered while paused. Note that this only works on hot observables.

#### Arguments
1. `pauser` *(`Observable`)*: The observable sequence used to pause the underlying sequence.

#### Returns
*(`Observable`)*: The observable sequence which is paused based upon the pauser.

#### Example
```js
var pauser = new Rx.Subject();
var source = Rx.Observable.interval(1000).pausableBuffered(pauser);

var subscription = source.subscribe(
    function (x) {
        console.log('Next: ' + x.toString());
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// To begin the flow
pauser.onNext(true); // or source.resume();

// To pause the flow at any point
pauser.onNext(false); // or source.pause();

// Resume the flow which empties the queue from when you last paused
pauser.onNext(true); // or source.resume();
```
