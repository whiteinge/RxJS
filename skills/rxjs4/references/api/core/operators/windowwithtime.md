### `Rx.Observable.prototype.windowWithTime(timeSpan, [timeShift | scheduler])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/windowwithtime.js "View in source")

Projects each element of an observable sequence into zero or more buffers which are produced based on timing information.

#### Arguments
1. `timeSpan` *(`Number`)*: Length of each buffer (specified as an integer denoting milliseconds).
2. `[timeShift]` *(`Number`)*: Interval between creation of consecutive buffers (specified as an integer denoting milliseconds).
3. `[scheduler=Rx.Scheduler.timeout]` *(`Scheduler`)*: Scheduler to run buffer timers on. If not specified, the timeout scheduler is used.

#### Returns
*(`Observable`)*: An observable sequence of buffers.

#### Example
```js
/* Without a skip */
var source = Rx.Observable.interval(100)
    .windowWithTime(500)
    .take(3);

var subscription = source.subscribe(
    function (child) {

        child.toArray().subscribe(
            function (x) {
                console.log('Child Next: ' + x.toString());
            },
            function (err) {
                console.log('Child Error: ' + err);
            },
            function () {
                console.log('Child Completed');
            }
        );
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Child Next: 0,1,2,3
// => Child Completed
// => Completed
// => Child Next: 4,5,6,7,8
// => Child Completed
// => Child Next: 9,10,11,12,13
// => Child Completed

/* Using a skip */
var source = Rx.Observable.interval(100)
    .windowWithTime(500, 100)
    .take(3);

var subscription = source.subscribe(
    function (child) {

        child.toArray().subscribe(
            function (x) {
                console.log('Child Next: ' + x.toString());
            },
            function (err) {
                console.log('Child Error: ' + err);
            },
            function () {
                console.log('Child Completed');
            }
        );
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Completed
// => Child Next: 0,1,2,3,4
// => Child Completed
// => Child Next: 0,1,2,3,4,5
// => Child Completed
// => Child Next: 1,2,3,4,5,6
// => Child Completed
```
