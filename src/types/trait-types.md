# Trait types

Trait types are opaque reference types unlike in the Rust language, therefore they can be used as the type of a variable, field or return value.

```ds
let trait_object: Trait = other_object;
```

_Downcast:_ Use `downcast!(v, T)` to cast trait object to a contravariant type:

```ds
if let Ok(bob) = downcast!(trait_object, Bob) {
    //
}
```

_Weak:_ A trait type may be combined with `Weak` to hold a weak reference.