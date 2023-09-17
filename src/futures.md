# Futures

DiveScript programs run asynchronously by nature. An opaque `Future` type is used for asynchronous operations.

```ds
// Locks the caller until completion
future().await;
```

All futures must be awaited for or be returned to a caller, or ignored:

```ds
let _ = future_in_the_background();
```