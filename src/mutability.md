# Mutability

Mutability is not transitive as in Rust. For example, a struct field is only mutable if such specific field has the `mut` qualifier.

```ds
struct S {
    mut n: f64,
}
```