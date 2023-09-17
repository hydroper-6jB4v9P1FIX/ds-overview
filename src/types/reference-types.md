# Reference types

All types, excluding primitives, are reference types using reference counting.

## Copy

Types are automatically copied if they implement `Copy`.

```ds
#[derive(Copy, CloneContent)]
struct S {
    x: f64 = 0.0,
}

fn main() {
    let s1 = S {};
    let s2 = s1; // copied
}
```

A type cannot implement `Copy` if it implements both `CloneContent` and `CloneReference`.

## Clone

A type is cloned either by content (the trait `CloneContent` and method `clone_content`) or by reference (the trait `CloneReference` and the method `clone_ref`). This distinguishment is necessary because the language supports reference types without the use of boxing types.

## Reference counting

Reference counting is a form of memory management that deallocates an object once it has zero references. A struct, enum or tuple is a reference type performing reference counting.

The following program demonstrates incrementing the field of a structure through a separate function:

```ds
struct S {
    mut x: f64 = 0.0,
}

fn main() {
    let object = S {};
    print!("First x: {}", object.x); // 0.0
    increment_x(object.clone_ref());
    print!("Final x: {}", object.x); // 1.0
}

fn increment_x(object: S) {
    object.x += 1.0;
}
```

Reference equality is tested for by using the auto implemented `RefEq` trait:

```ds
object.ref_eq(another_object);
object.ref_ne(another_object);
```

## Circular references

With reference counting, when an object can reference to another object recursively, a memory leak can occur since the reference count may never reach zero.

`Weak<T>` allows to hold a _weak_ reference to an object, which does not count as a reference to the original object. It is obtained via `Weak::from(object)` and an attempt to upgrade it back to a `T` is possible via `weak.upgrade()`.

`Weak<T>` can be often used to hold a _weak_ reference to a parent object:

```ds
struct Graph {
    mut parent: Weak<Graph> = Weak::empty(),
    children: [Graph] = [],
}
```