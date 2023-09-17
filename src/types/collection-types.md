# Collection types

## Array

Arrays are insertion-order lists that can alter in size at any point in the program.

```ds
let array: [str] = ["foo"];
// appends string "bar" to the array
array.push("bar");
assert_eq!(["foo", "bar"], array);
```

## Map

The most common type for storing key-value pairs is `HashMap`, however the `map!` macro can initialize any type that can be constructed from key-value pairs.

```ds
type M = HashMap<str, f64>;
let map: M = map! {
    "x" => 10.0,
    "y => 5.0,
};
```