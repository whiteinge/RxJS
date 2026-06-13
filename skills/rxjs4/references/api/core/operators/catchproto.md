### `Rx.Observable.prototype.catch(second | handler)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/dist/rx.js#L3107-L3112 "View in source")

Continues an observable sequence that is terminated by an exception with the next observable sequence.

#### Arguments

Using another Observable:
- `second` *(`Observable`)*: A second observable sequence used to produce results when an error occurred in the first sequence.

Using a handler:
- `handler` *(`Function`)*: Exception handler function that returns an observable sequence given the error that occurred in the first sequence

#### Returns
*(`Observable`)*: An observable sequence containing the first sequence's elements, followed by the elements of the handler sequence in case an exception occurred.

#### Example
```js
/* Using a second observable */
var source = Rx.Observable.throw(new Error()).catch(Rx.Observable.just(42));

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

/* Using a handler function */
var source = Rx.Observable.throw(new TimeoutError())
    .catch(function (e) {
      var returnValue;
      if (e instanceof TimeoutError) { return Rx.Observable.just(42); }
      return Rx.Observable.throw(e);
    });

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
