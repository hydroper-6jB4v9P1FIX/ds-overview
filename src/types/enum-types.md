# Enum types

## Tagging

```ds
#[derive(PartialEq, Copy, CloneContent)]
#[discriminant(str)]
enum E {
    X = "x",
    Y = "y",
}
```