# `Rx.Scheduler` class #

Provides a set of static methods to access commonly used schedulers and a base class for all schedulers.

## Usage ##

The follow example shows the basic usage of an `Rx.Scheduler`.

```js
var disposable = Rx.Scheduler.default.schedule(
  'world',
  function (scheduler, x) { console.log('hello ' + x); }
);

// => hello world
```
