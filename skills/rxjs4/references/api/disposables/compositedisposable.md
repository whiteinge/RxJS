# `Rx.CompositeDisposable` class #

Represents a group of disposable resources that are disposed together.

## Usage ##

The follow example shows the basic usage of an Rx.CompositeDisposable.

```js
var d1 = Rx.Disposable.create(function () {
     console.log('one');
});

var d2 = Rx.Disposable.create(function () {
     console.log('two');
});

// Initialize with two disposables
var disposables = new Rx.CompositeDisposable(d1, d2);

disposables.dispose();
// => one
// => two
```
