# `Rx.RefCountDisposable` class #

Represents a disposable resource that only disposes its underlying disposable resource when all `getDisposable` dependent disposable objects have been disposed.

## Usage ##

The follow example shows the basic usage of an `Rx.RefCountDisposable`.

```js
var disposable = Rx.Disposable.create(function () {
     console.log('disposed');
});

var refCountDisposable = new Rx.RefCountDisposable(disposable);

var disposable1 = refCountDisposable.getDisposable();
var disposable2 = refCountDisposable.getDisposable();

disposable1.dispose();
console.log(disposable.isDisposed);
// => false

disposable2.dispose();
console.log(disposable.isDisposed);
// => false

refCountDisposable.dispose();
// => disposed

console.log(refCountDisposable.isDisposed);
// => true
```
