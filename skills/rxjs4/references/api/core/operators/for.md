### `Rx.Observable.for(sources, resultSelector, [thisArg])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/tests/observable/for.js "View in source")

Concatenates the observable sequences or Promises obtained by running the specified result selector for each element in source.
There is an alias for this method called `forIn` for browsers <IE9

#### Arguments
1. `sources` *(Array)*: An array of values to turn into an observable sequence.
2. `resultSelector` *(`Function`)*: A function to apply to each item in the sources array to turn it into an observable sequence. The resultSelector is called with the following information:
    1. the value of the element
    2. the index of the element
    3. the Observable object being subscribed

3. `[thisArg]` *(`Any`)*: Object to use as `this` when executing `resultSelector`.

#### Returns
*(`Observable`)*: An observable sequence from the concatenated observable sequences or Promises.

#### Example
```js
/* Using Observables */
var array = [1, 2, 3];

var source = Rx.Observable.for(
    array,
    function (x) {
        return Rx.Observable.return(x);
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

// => Next: 1
// => Next: 2
// => Next: 3
// => Completed

/* Using Promises */
var array = [1, 2, 3];

var source = Rx.Observable.for(
    array,
    function (x) {
        return RSVP.Promise.resolve(x);
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

// => Next: 1
// => Next: 2
// => Next: 3
// => Completed
```
