# Dynamic typing

`Any` is a type from which any type implementing `Copy` implicitly converts to. It includes two methods: `is<T>` and `downcast<T>`. During conversion from `T` to `Any`, if `T: CloneReference`, `clone_ref` is used to clone; otherwise `CloneContent` is used.