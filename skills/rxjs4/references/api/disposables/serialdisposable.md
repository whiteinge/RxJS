# `Rx.SerialDisposable` class #

Represents a disposable resource whose underlying disposable resource can be replaced by another disposable resource, causing automatic disposal of the previous underlying disposable resource.

## Usage ##

The follow example shows the basic usage of an Rx.SerialDisposable.

```js
var serialDisposable = new Rx.SerialDisposable();

var d1 = Rx.Disposable.create(function () {
     console.log('one');
});

serialDisposable.setDisposable(d1);

var d2 = Rx.Disposable.create(function () {
     console.log('two');
});

serialDisposable.setDisposable(d2);
// => one

serialDisposable.dispose();
// = two
```
