# Option and Result types

## Try block

The `try` block is used for optionally chaining operations on `Option` or `Result` in a new scope:

```ds
try { some_option?.f().x }
```