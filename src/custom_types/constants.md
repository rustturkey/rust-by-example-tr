# sabitler

Rust, global dahil herhangi bir kapsamda bildirilebilen iki farklı sabit tipini içerir. Her ikisi de açık tip ek açıklaması gerektirirler:

* `const`: Değişmez değer. (ortak durum).
* `static`:  [`'static`][static] ömre sahip `mut`able(değişebilir) değişken.
  Statik ömür çıkarılır yani belirtilmesi gerekmez.
  Mutable bir statik değişkene erişmek veya üzerinde değişiklik yapmak [`güvensiz işlem`][unsafe]dir.

```rust,editable,ignore,mdbook-runnable
// Global değişkenler tüm kapsamların dışında bildirilir.
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    //Herhangi bir fonksiyondan sabit'e erişim
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // Ana thread'den sabit'e erişim
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
    println!("{} is {}", n, if is_big(n) { "big" } else { "small" });

    // Hata! `const` yani sabit değişemez.
    THRESHOLD = 5;
    // FIXME ^ Yorum satırı
}
```

### Ayrıca bakın:

[`const`/`static` RFC](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[`'static` ömür][static]

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md
