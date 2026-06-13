### `Rx.Observable.startAsync(functionAsync)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/startasync.js "View in source")

Invokes the asynchronous function, surfacing the result through an observable sequence.

### Arguments
1. `functionAsync` *(`Function`)*: Asynchronous function which returns a Promise to run.

#### Returns
*(`Observable`)*: An observable sequence exposing the function's Promises's value or error.

#### Example
```js
var source = Rx.Observable.startAsync(function () {
    return RSVP.Promise.resolve(42);
});

var subscription = source.subscribe(
    function (x) {
        console.log('Next: ' + x);
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Next: 42
// => Completed
```
