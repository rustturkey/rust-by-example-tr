# `dead_code`

Derleyici, kullanılmayan fonksiyonlar hakkında uyarı verecek bir `dead_code`
[*lint'i*][lint] sağlar. Bir *özellik* lint'i devre dışı bırakmak için kullanılabilir.

```rust,editable
fn used_function() {}

// `#[allow(dead_code)]` , `dead_code` lint'ini devre dışı bırakan bir özelliktir
#[allow(dead_code)]
fn unused_function() {}

fn noisy_unused_function() {}
// FIXME(Daha iyi yapılabilir) ^ Uyarıyı bastırmak için bir özellik ekleyin

fn main() {
    used_function();
}
```

Gerçek programlamalarda dead code(ölü kod)'u ortadan kaldırmanız gerektiğini unutmayın. Bu örneklerde, örneklerin etkileşimli doğası nedeniyle bazı yerlerde ölü koda izin vereceğiz.

[lint]: https://en.wikipedia.org/wiki/Lint_%28software%29
