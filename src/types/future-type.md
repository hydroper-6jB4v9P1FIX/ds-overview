# Future type

An opaque `Future<T>` type is used for asynchronous operations. It is the same mechanism from JavaScript `Promise`s.

```ds
// Locks the caller until completion
future().await;
```

A future must be awaited for or be returned to a caller, or ignored:

```ds
let _ = future_in_the_background();
```

More examples on future usage:

```ds
let _ = Future::ready(Ok("value"));

fn f() -> Future<str> {
    Future::ready("value")
}

let (result, index) = Future::race(future_list);

fn f() -> Future<u64> {
    Future::new(|resolve, _reject| {
        resolve(10);
    })
}
```