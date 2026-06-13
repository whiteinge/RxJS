### `Rx.Observable.return(value, [scheduler])` ###
### `Rx.Observable.just(value, [scheduler])` ###
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/perf/operators/just.js "View in source")

Returns an observable sequence that contains a single element, using the specified scheduler to send out observer messages.

There is an alias called `returnValue` for browsers <IE9 and a regular alias called `just`.

### Arguments
1. `value` *(`Any`)*: Single element in the resulting observable sequence.
2. `[scheduler=Rx.Scheduler.immediate]` *(`Scheduler`)*: Scheduler to send the single element on. If not specified, defaults to Scheduler.immediate.

#### Returns
*(`Observable`)*: An observable sequence with the single element.

#### Example
```js
var source = Rx.Observable.just(42);

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
