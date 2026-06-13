### `Rx.Observable.prototype.switchFirst()` ##
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/switchfirst.js "View in source")

Receives an `Observable` of `Observables` and propagates the first `Observable` exclusively until it completes before it begins subscribes to the next `Observable`.  Observables that come before the current Observable completes will be dropped and will not propagate.

This operator is similar to `concatAll()` except that it will not hold onto Observables that come in before the current one is finished completed.

#### Returns
*(`Observable`)*: An Observable sequence that is the result of concatenating non-overlapping items emitted by an Observable of Observables.

#### Example

```javascript

//Generate an event every 100 milliseconds
var source = Rx.Observable.generateWithRelativeTime(
   0,
   function(x) {return x < 5; },
   function(x) {return x + 1; },
   function(x) {return x; },
   function(x) {return 100; })
  .map(function(value) {
    //Observable takes 150 milliseconds to complete
    return Rx.Observable.timer(150).map(value);
  });

source.exclusive().subscribe(
   function (x) {
    console.log("Next %d", x);
   }, function(e) {
    console.log("Error %s", e);
   }, function() {
    console.log("Completed");
   });

// Next 0
// Next 2
// Next 4
// Completed
```
