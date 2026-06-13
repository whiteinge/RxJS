### `Rx.Observable.toPromise([promiseCtor])`
[&#x24C8;](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/topromise.js "View in source")

Converts an Observable sequence to a ES2015 compliant promise.

#### Arguments
1. `[promiseCtor]` *(Promise)*: An ES2015 compliant Promise that can be created.  This is optional.  If your runtime already supports ES2015 promises, you do not need to fill in this parameter.  Alternatively you can specify an ES2015 complaint promise via `Rx.config.Promise`

#### Returns
*(`Promise`)*: An ES2015 compliant promise which contains the last value from the Observable sequence. If the Observable sequence is in error, then the Promise will be in the rejected stage. If the sequence is empty, the Promise will not resolve.

#### Example
```es6
/* Using normal ES2015 */
let source = Rx.Observable
  .just(42)
  .toPromise();

source.then((value) => console.log('Value: %s', value));
// => Value: 42

/* Rejected Promise */
/* Using normal ES2015 */
let source = Rx.Observable
  .throw(new Error('woops'))
  .toPromise();

source
  .then((value) => console.log('Value: %s', value))
  .catch((err) => console.log('Error: %s', err));
// => Error: Error: woops

/* Setting via the config */
Rx.config.Promise = RSVP.Promise;

let source = Rx.Observable
  .just(42)
  .toPromise();

source.then((value) => console.log('Value: %s', value));
// => Value: 42

/* Setting via the method */
let source = Rx.Observable
  .just(42)
  .toPromise(RSVP.Promise);

source.then((value) => console.log('Value: %s', value));
// => Value: 42
```
