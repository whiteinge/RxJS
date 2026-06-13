# `Rx.Disposable` class #

Provides a set of static methods for creating Disposables, which defines a method to release allocated resources.

## Usage ##

The follow example shows the basic usage of an `Rx.Disposable`.

```js
var disposable = Rx.Disposable.create(function () {
    console.log('disposed');
});

disposable.dispose();
// => disposed
```

## `Disposable Class Methods` ##
- [`create`](#rxdisposablecreateaction)
- [`isDisposable`](#rxdisposableisdisposabled)

## `Disposable Class Properties` ##
- [`empty`](#rxdisposableempty)

## `Disposable Instance Methods` ##
- [`dispose`](#rxdisposableprototypedispose)

## _Class Methods_ ##

### <a id="rxdisposablecreateaction"></a>`Rx.Disposable.create(action)`
<a href="#rxdisposablecreateaction">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/disposables/disposable.js"View in source")

Creates a disposable object that invokes the specified action when disposed.

#### Arguments
1. `action` *(Function)*: Function to run during the first call to `dispose`. The action is guaranteed to be run at most once.

#### Returns
*(Disposable)*: The disposable object that runs the given action upon disposal.

#### Example
```js
var disposable = Rx.Disposable.create(function () {
    console.log('disposed');
});

disposable.dispose();
// => disposed
```
