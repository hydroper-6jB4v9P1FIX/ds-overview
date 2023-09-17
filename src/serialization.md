# Serialization

DiveScript comes with a basic form of serialization for JSON, shortened to “ser”.

```ds
#[derive(Serializable)]
struct S {
    n: bigint,
}

#[derive(Serializable)]
#[discriminant(str)]
#[ser(tag = "type")]
enum E {
    Variant { n: bigint } = "variant",
}

#[derive(Serializable)]
#[discriminant(str)]
enum E2 {
    Variant = "variant",
}
```