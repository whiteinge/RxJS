# `Rx.VirtualTimeScheduler` class #

Base class for providing scheduling in virtual time.  This inherits from the `Rx.Scheduler` class.

## Usage ##

The following shows an example of using the `Rx.VirtualTimeScheduler`. In order for this to work, you must implement the `add`, `toAbsoluteTime` and `toRelativeTime` methods as described below.

```js
/* Comparer required for scheduling priority */
function comparer (x, y) {
  if (x > y) { return 1; }
  if (x < y) { return -1; }
  return 0;
}

var scheduler = new Rx.VirtualTimeScheduler(0, comparer);

/**
 * Adds a relative time value to an absolute time value.
 * @param {Any} absolute Absolute virtual time value.
 * @param {Any} relative Relative virtual time value to add.
 * @return {Any} Resulting absolute virtual time sum value.
 */
scheduler.add = function (absolute, relative) {
  return absolute + relative;
};

/**
 * Converts an absolute time to a number
 * @param {Number} The absolute time in ms
 * @returns {Number} The absolute time in ms
 */
scheduler.toAbsoluteTime = function (absolute) {
  return new Date(absolute);
};

/**
 * Converts the time span number/Date to a relative virtual time value.
 * @param {Number} timeSpan TimeSpan value to convert.
 * @return {Number} Corresponding relative virtual time value.
 */
scheduler.toRelativeTime = function (timeSpan) {
  return timeSpan;
};

// Schedule some time
scheduler.scheduleAbsolute(null, new Date(1), function () { console.log('foo'); });
scheduler.scheduleAbsolute(null, new Date(2), function () { console.log('bar'); });
scheduler.scheduleAbsolute(null, new Date(3), function () { scheduler.stop(); });

// Start the scheduler
scheduler.start();

// => foo
// => bar

// Check the clock once stopped
console.log(scheduler.now());
// => 3

console.log(scheduler.clock);
// => 3
```
