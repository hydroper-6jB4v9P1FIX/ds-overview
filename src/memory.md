# Memory

All types are passed by value by default.

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

Using types as reference types is normally done via reference counting.

Reference counting is a form of memory management that deallocates an object once it has zero references. The language supports the attribute `rc`, indicating that a struct or enum is a reference type performing reference counting.

The following program demonstrates incrementing the field of a structure through a separate function:

```ds
#[rc]
struct S {
    mut x: f64 = 0.0,
}

fn main() {
    let object = S {};
    print!("First x: {}", object.x);
    increment_x(object.clone_ref());
    print!("Final x: {}", object.x);
}

fn increment_x(object: S) {
    object.x += 1.0;
}
```

The native `rc_eq!` and `rc_ne!` macros may be necessary when working with reference counting to distinguish reference from actual content or, alternatively, the `RcEq` derive attribute can be used:

```ds
#[rc]
#[derive(RcEq)]
struct S;
```

## Circular references

With reference counting, when an object can reference to another object recursively, a memory leak can occur since the reference count may never reach zero.

`Weak<T>` allows to hold a _weak_ reference to an object, which does not count as a reference to the original object. It is obtained via `Weak::from(object)` and an attempt to upgrade it back to a `T` is possible via `weak.upgrade()`.

`Weak<T>` can be often used to hold a _weak_ reference to a parent object:

```ds
#[rc]
struct Graph {
    mut parent: Weak<Graph> = Weak::empty(),
    children: [Graph] = [],
}
```