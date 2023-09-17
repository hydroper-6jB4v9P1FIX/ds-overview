# Macros

## Method macros

Method macros are always applied to an instance (the `__self` variable in their scope).

```ds
impl S {
    pub macro f {
        () => {
            __self.f2()
        },
    }

    pub fn f2(self) -> f64 {
        0.0
    }
}
```