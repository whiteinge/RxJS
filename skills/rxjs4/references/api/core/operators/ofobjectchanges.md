### `Rx.Observable.ofObjectChanges(obj)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/ofobjectchanges.js "View in source")

Creates an Observable sequence from changes to an object using `Object.observe`.

#### Arguments
1. `array` *(`Array`)*: The object to observe changes using `Object.observe`

#### Returns
*(`Observable`)*: An observable sequence containing changes to an object from `Object.observe`.

#### Example
```js
var obj = {x: 1};
var source = Rx.Observable.ofObjectChanges(obj);

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

obj.x = 42;

// => Next: {type: "update", object: Object, name: "x", oldValue: 1}
```
