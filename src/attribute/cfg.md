# `cfg`

Konfigürasyon koşullu kontrolleri iki farklı operatör aracılığıyla mümkündür:

* `cfg` özelliği: `#[cfg(...)]` özellik konumundayken
* `cfg!` macro'su: `cfg!(...)` boolean ifadeyken

Birincisi koşullu derlemeyi mümkün kılarken, ikincisi koşullu olarak `true`(doğru) veya `false`(yanlış) değişmez değerlerle çalışma zamanında kontrollere izin verir. Her ikisi de aynı söz dizimini kullanır.

```rust,editable
// Bu fonksiyon yalnızca hedef işletim sistemi linux ise derlenir
#[cfg(target_os = "linux")]
fn are_you_on_linux() {
    println!("You are running linux!");
}

// Ve bu fonksiyon yalnızca hedef işletim sistemi linux *değilse* derlenir
#[cfg(not(target_os = "linux"))]
fn are_you_on_linux() {
    println!("You are *not* running linux!");
}

fn main() {
    are_you_on_linux();

    println!("Are you sure?");
    if cfg!(target_os = "linux") {
        println!("Yes. It's definitely linux!");
    } else {
        println!("Yes. It's definitely *not* linux!");
    }
}
```

### Ayrıca bakın:

[İngilizce referans][ref], [`cfg!`][cfg], ve [macro'lar][macros].

[cfg]: https://doc.rust-lang.org/std/macro.cfg!.html
[macros]: ../macros.md
[ref]: https://doc.rust-lang.org/reference/attributes.html#conditional-compilation
