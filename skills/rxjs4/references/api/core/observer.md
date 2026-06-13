# Observer object #

The Observer object provides support for push-style iteration over an observable sequence.

The Observer and Objects interfaces provide a generalized mechanism for push-based notification, also known as the observer design pattern. The Observable object represents the object that sends notifications (the provider); the Observer object represents the class that receives them (the observer).

<!-- div -->

## `Observer Methods`
- [`create`](#rxobservercreateonnext-onerror-oncompleted)
- [`fromNotifier`](#rxobserverfromotifierhandler)

## `Observer Instance Methods`
- [`asObserver`](#rxobserverprototypeasobserver)
- [`checked`](#rxobserverprototypechecked)
- [`notifyOn`](#rxobserverprototypenotifyonscheduler)
- [`onCompleted`](#rxobserverprototypeoncompleted)
- [`onError`](#rxobserverprototypeonerrorerror)
- [`onNext`](#rxobserverprototypeonnextvalue)
- [`toNotifier`](#rxobserverprototypetonotifier)

## _Observer Methods_ ##

### <a id="rxobservercreateonnext-onerror-oncompleted"></a>`Rx.Observer.create([onNext], [onError], [onCompleted])`
<a href="#rxobservercreateonnext-onerror-oncompleted">#</a> [&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/dist/rx.js#L1828-L1833 "View in source") [&#x24C9;][1]

Creates an observer from the specified `onNext`, `onError`, and `onCompleted` actions.

#### Arguments
1. `[onNext]` *(Function)*: Observer's onNext action implementation.
2. `[onError]` *(Function)*: Observer's onError action implementation.
3. `[onCompleted]` *(Function)*: Observer's onCompleted action implementation.

#### Returns
*(Observer)*: The observer object implemented using the given actions.

#### Example
```js
var source = Rx.Observable.return(42);

var observer = Rx.Observer.create(
    function (x) {
        console.log('Next: ' + x);
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    }
);

var subscription = source.subscribe(observer);

// => Next: 42
// => Completed
```
