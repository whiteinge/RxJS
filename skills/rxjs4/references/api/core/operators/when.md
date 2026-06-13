### `Rx.Observable.when(...args)`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/when.js "View in source")

A series of plans (specified as an Array or as a series of arguments) created by use of the Then operator on patterns.

### Arguments
1. `args` *(arguments|Array)*: A series of plans (specified as an Array of as a series of arguments) created by use of the then operator on patterns.

#### Returns
*(`Observable`)*: Observable sequence with the results form matching several patterns.

#### Example
```js
// Fire each plan when both are ready
var source = Rx.Observable.when(
  Rx.Observable.timer(100).and(Rx.Observable.timer(500)).thenDo(function (x, y) { return 'first'; }),
  Rx.Observable.timer(400).and(Rx.Observable.timer(300)).thenDo(function (x, y) { return 'second'; })
);

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

// => Next: second
// => Next: first
// => Completed
```

#### Example

```js
var chopsticks = [new Rx.Subject(), new Rx.Subject(), new Rx.Subject()];

var hungry = [new Rx.Subject(), new Rx.Subject(), new Rx.Subject()];

var eat = i => {
  return () => {
    setTimeout(() => {
      console.log('Done');
      chopsticks[i].onNext({});
      chopsticks[(i+1) % 3].onNext({});
    }, 1000);
    return 'philosopher ' + i + ' eating';
  };
};

var dining = Rx.Observable.when(
  hungry[0].and(chopsticks[0]).and(chopsticks[1]).thenDo(eat(0)),
  hungry[1].and(chopsticks[1]).and(chopsticks[2]).thenDo(eat(1)),
  hungry[2].and(chopsticks[2]).and(chopsticks[0]).thenDo(eat(2))
);

dining.subscribe(console.log.bind(console));

chopsticks[0].onNext({}); chopsticks[1].onNext({}); chopsticks[2].onNext({});

for (var i = 0; i < 3; i++) {
  hungry[0].onNext({}); hungry[1].onNext({}); hungry[2].onNext({});
}
```
