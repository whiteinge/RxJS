---
name: rxjs4
description: RxJS v4 (Reactive-Extensions/RxJS) — the archived, dot-chaining Rx API, NOT the pipe()-based RxJS 5+. Use when writing or reviewing RxJS v4 observable chains and unsure whether an operator exists, what its exact v4 name or signature is (v5+ names like switchMap, mergeMap, catchError, debounceTime do not exist in v4), or when working with v4 Subjects, Disposables, Schedulers, or the TestScheduler.
license: Apache-2.0
metadata:
  author: Microsoft Open Technologies / ReactiveX contributors
  version: "4.1.0"
  repository: https://github.com/Reactive-Extensions/RxJS
allowed-tools: Read
---

# RxJS v4

RxJS v4 is the final release line of `Reactive-Extensions/RxJS`. The upstream repo is archived, so this API is frozen — these docs are complete and will never be out of date.

This is a **different API** from the RxJS 5/6/7 (`ReactiveX/rxjs`) that dominates tutorials and training data. Do not carry v5+ idioms into v4 code:

- Operators are **dot-chained** on the observable: `source.map(fn).filter(fn).flatMapLatest(fn)`. There is no `.pipe()` and there are no standalone lettable operators. (`.let(fn)` exists for chaining a function over the whole sequence.)
- `subscribe()` returns a **Disposable** — call `.dispose()`, not `.unsubscribe()`.
- Many operators accept an optional trailing **`resultSelector`** and/or **scheduler** argument that v5+ dropped — check the signature before assuming arity.
- Time-based operators take the duration directly (`debounce(500)`); there are no separate `*Time` variants.

## Looking things up

1. **Check the host project's Rx extensions first.** Projects commonly extend `Rx.Observable.prototype` with custom operators (e.g. an `rxext` layer exposing `Rx.EXT`); a project-local operator or convention wins over the stock API.
2. **[`references/operator-index.md`](references/operator-index.md)** — every static and instance method with its exact v4 signature, a one-line description, and a link to the full doc. Grep this first to confirm an operator exists and to catch aliases (`map`/`select`, `filter`/`where`, `tap`/`do`, `flatMap`/`selectMany`, `just`/`return`).
3. **`references/api/core/operators/<name>.md`** — full doc per operator (lowercase filename): arguments incl. callback parameters, return value, runnable example. Instance variants of dual static/instance operators use a `proto` suffix (`concat.md` vs `concatproto.md`).
4. **`references/api/`** — non-operator APIs: [`core/observable.md`](references/api/core/observable.md) (method lists), [`core/observer.md`](references/api/core/observer.md), [`core/notification.md`](references/api/core/notification.md), plus `subjects/`, `disposables/`, `schedulers/`, `testing/`, `helpers/`, `config/`.
5. **`references/guides/`** — conceptual guides: operator categories, "which operator do I use" decision tables (`which-static.md`, `which-instance.md`), creating/querying sequences, subjects, schedulers, testing, backpressure, transducers.
6. **`references/howdoi/`** — recipes, including [`createcustomoperators.md`](references/howdoi/createcustomoperators.md) for adding operators to `Rx.Observable.prototype`.

## v5+ name → v4 name

The renames most likely to trip up someone fluent in modern RxJS. None of the left-column names exist in v4.

| RxJS 5+ | RxJS v4 |
|---|---|
| `pipe(op1(), op2())` | dot-chain: `.op1().op2()` |
| `switchMap` | `flatMapLatest` |
| `mergeMap` | `flatMap` (alias `selectMany`) |
| `exhaustMap` | `flatMapFirst` |
| `mergeMap` with concurrency | `flatMapWithMaxConcurrent` |
| `catchError` | `catch` |
| `finalize` | `finally` |
| `do` → `tap` (v5) | both `do` and `tap` exist |
| `debounceTime(ms)` | `debounce(ms)` |
| `throttleTime(ms)` | `throttle(ms)` |
| `audit` / `auditTime` | `sample` / `debounce` variants (no direct equivalent) |
| `bufferTime` / `bufferCount` | `bufferWithTime` / `bufferWithCount` |
| `windowTime` / `windowCount` | `windowWithTime` / `windowWithCount` |
| `race` | `amb` |
| `mapTo(x)` | `map(() => x)` (no `mapTo`) |
| `switchAll` | `switch` (alias `switchLatest`) |
| `exhaust` | `switchFirst` |
| `publishReplay` | `replay` |
| `subscription.unsubscribe()` | `disposable.dispose()` |

## Operators by task

Names only — exact signatures are in [`references/operator-index.md`](references/operator-index.md).

- **Creating**: `create`, `defer`, `empty`, `generate`, `generateWithAbsoluteTime`, `generateWithRelativeTime`, `interval`, `just`/`return`, `never`, `of`, `ofWithScheduler`, `pairs`, `range`, `repeat` (static), `start`, `startAsync`, `throw`, `timer`, `using`, `wrap` (generators), `spawn`, `toAsync`
- **From other sources**: `from`, `fromArray`, `fromCallback`, `fromNodeCallback`, `fromEvent`, `fromEventPattern`, `fromPromise`; back out via `toArray`, `toMap`, `toSet`, `toPromise`
- **Transforming**: `map`/`select`, `pluck`, `flatMap`/`selectMany`, `flatMapLatest`, `flatMapFirst`, `flatMapWithMaxConcurrent`, `concatMap`/`selectConcat`, `scan`, `expand`, `manySelect`/`extend`, `materialize`/`dematerialize`, `timeInterval`, `timestamp`, `transduce`
- **Filtering**: `filter`/`where`, `distinct`, `distinctUntilChanged`, `elementAt`, `find`, `findIndex`, `first`, `last`, `single`, `ignoreElements`, `sample`, `skip`, `skipLast`, `skipUntil`, `skipWhile`, `slice`, `take`, `takeLast`, `takeUntil`, `takeWhile`, `debounce`, `throttle` (plus `*WithTime` variants of skip/take)
- **Combining**: `amb`, `combineLatest`, `concat`, `concatAll`, `forkJoin`, `merge`, `mergeAll`, `mergeDelayError`, `startWith`, `switch`/`switchLatest`, `switchFirst`, `withLatestFrom`, `zip`, `zipIterable`, `pairwise`; join calculus via `join`, `groupJoin`, `when`/`and`/`thenDo`
- **Grouping, buffers, windows**: `groupBy`, `groupByUntil`, `partition`, `buffer`, `bufferWithCount`, `bufferWithTime`, `bufferWithTimeOrCount`, `window`, `windowWithCount`, `windowWithTime`, `windowWithTimeOrCount`, `takeLastBuffer`
- **Error handling**: `catch`, `finally`, `onErrorResumeNext`, `retry`, `retryWhen`, `repeat` (instance), `repeatWhen`, `timeout`, `timeoutWithSelector`
- **Sharing & multicast**: `multicast`, `publish`, `publishLast`, `publishValue`, `replay`, `share`, `shareReplay`, `shareValue`, `refCount`, `connect`, `singleInstance`, `asObservable`, `let`
- **Backpressure**: `controlled`, `pausable`, `pausableBuffered` (see [`references/guides/backpressure.md`](references/guides/backpressure.md))
- **Aggregation & predicates**: `average`, `count`, `max`, `maxBy`, `min`, `minBy`, `reduce`, `sum`, `every`, `some`, `includes`, `indexOf`, `lastIndexOf`, `isEmpty`, `sequenceEqual`, `defaultIfEmpty`
- **Side effects & scheduling**: `tap`/`do` (+ `tapOnNext`/`tapOnError`/`tapOnCompleted`), `subscribe`/`forEach`, `subscribeOn`, `observeOn`, `delay`, `delaySubscription`

## Other APIs

- **Subjects** (`references/api/subjects/`): [`Subject`](references/api/subjects/subject.md), [`AsyncSubject`](references/api/subjects/asyncsubject.md), [`BehaviorSubject`](references/api/subjects/behaviorsubject.md), [`ReplaySubject`](references/api/subjects/replaysubject.md)
- **Disposables** (`references/api/disposables/`): [`Disposable`](references/api/disposables/disposable.md), [`CompositeDisposable`](references/api/disposables/compositedisposable.md), [`SerialDisposable`](references/api/disposables/serialdisposable.md), [`SingleAssignmentDisposable`](references/api/disposables/singleassignmentdisposable.md), [`RefCountDisposable`](references/api/disposables/refcountdisposable.md)
- **Schedulers** (`references/api/schedulers/`): [`Scheduler`](references/api/schedulers/scheduler.md) (incl. `Rx.Scheduler.immediate`, `.currentThread`, `.default`), [`VirtualTimeScheduler`](references/api/schedulers/virtualtimescheduler.md), [`HistoricalScheduler`](references/api/schedulers/historicalscheduler.md)
- **Testing** (`references/api/testing/`): [`TestScheduler`](references/api/testing/testscheduler.md), [`ReactiveTest`](references/api/testing/reactivetest.md) (`onNext`/`onError`/`onCompleted` factories), [`Recorded`](references/api/testing/recorded.md), [`Subscription`](references/api/testing/subscription.md) — note v4 has no marble-string syntax; tests record `(ticks, value)` pairs via a `TestScheduler`

## Regenerating

`references/` is generated from this repo's `doc/` tree by [`skills/build.js`](../build.js) (strips per-file boilerplate, extracts the operator index). The upstream repo is archived, so regeneration should only ever be needed if the extraction itself changes.
