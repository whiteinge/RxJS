### `Rx.Observable.prototype.pluck(property)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/pluck.js#L10 "View in source")

Returns an Observable containing the value of a specified nested property from
all elements in the Observable sequence. If a property can't be resolved, it
will return `undefined` for that value.

#### Arguments
1. `property` *(`String`)*: The property or properties to pluck. `pluck`
   accepts an unlimited number of nested property parameters.

#### Returns
*(`Observable`)*: Returns a new Observable sequence of property values.

#### Example
```js
var source = Rx.Observable
    .from([
        { value: 0 },
        { value: 1 },
        { value: 2 }
    ])
    .pluck('value');

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

// => Next: 0
// => Next: 1
// => Next: 2
// => Completed

// Using nested properties:

var source = Rx.Observable
    .from([
        { valueA: { valueB: { valueC: 0 }}},
        { valueA: { valueB: { valueC: 1 }}},
        { valueA: { valueB: 2 }},
    ])
    .pluck('valueA', 'valueB', 'valueC');

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

// => Next: 0
// => Next: 1
// => Next: undefined
// => Completed
```
