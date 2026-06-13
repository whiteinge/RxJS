# `Rx.SingleAssignmentDisposable` class #

Represents a disposable resource which only allows a single assignment of its underlying disposable resource. If an underlying disposable resource has already been set, future attempts to set the underlying disposable resource will throw an Error.

## Usage ##

The follow example shows the basic usage of an Rx.SingleAssignmentDisposable.

```js
var singleDisposable = new Rx.SingleAssignmentDisposable();

var disposable = Rx.Disposable.create(function () {
     console.log('disposed');
});

singleDisposable.setDisposable(disposable);

singleDisposable.dispose();
// => disposed
```
