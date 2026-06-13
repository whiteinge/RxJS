# Notification object #

Represents a notification to an observer.

## Usage ##

This can be dematerialized into an Observable.
```js
var source = Rx.Observable
  .of(
    Rx.Notification.createOnNext(42),
    Rx.Notification.createOnCompleted()
  )
  .dematerialize();

var subscription = source.subscribe(
  function (x) {
    console.log('Next: %s', x);
  },
  function (err) {
    console.log('Error: %s', err);
  },
  function () {
    console.log('Completed');
  });

// => Next: 42
// => Completed
```
