# Temeller

Rust çok çeşitli `temeller`e (primitive) erişim sağlar. İçeren bir örnek:


### Skaler(Sayısal) Tipler

* işaretli tamsayılar: `i8`, `i16`, `i32`, `i64`, `i128` and `isize` (pointer(işaretçi) boyutu)
* işaretsiz tamsayılar: `u8`, `u16`, `u32`, `u64`, `u128` and `usize` (pointer(işaretçi)
  boyutu)
* kayar noktalı sayılar: `f32`, `f64`
* `char` Uluslararası dil desteği sayısallar `'a'`, `'α'` ve `'∞'` (her biri 4 byte)
* `bool`  `true` (doğru değeri) veya `false` (yanlış değeri)
* ve birim tipi `()`, tek olası değeri boş değişken grubu: `()`

Bir birim tipinin değeri bir boş değişken grubu olmasına rağmen, birden çok değer içermediği için birleşik tip olarak kabul edilemez.

### Birleşik Tipler

* diziler şöyledir: `[1, 2, 3]`
* değişken grupları şöyledir: `(1, true)`

Değişkenler her zaman *tip açıklamalı* olabilirler. Numaralara ek olarak bir *son ek* veya *varsayılan* şekilde bir açıklama eklenebilir. Tamsayılar varsayılan olarak `i32` 'dir
ve kayar noktalı sayılar `f64`. Rust'ın tipleri bağlamdan da çıkarabileceğini unutmayın.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Değişkenler tip açıklamalı olabilir.
    let logical: bool = true;

    let a_float: f64 = 1.0;  // Sıradan açıklama
    let an_integer   = 5i32; // Son ek ile açıklama

    // Ya da varsayılan kullanılabilir.
    let default_float   = 3.0; // `f64`
    let default_integer = 7;   // `i32`
    
    // Tip bağlamdan da çıkarılabilir. 
    let mut inferred_type = 12; // i64 başka satırdan anlaşılmıştır
    inferred_type = 4294967296i64;
    
    // Mutable(değişebilir) değişkenin değeri değişebilir.
    let mut mutable = 12; // Değişebilir `i32`
    mutable = 21;
    
    // Hata! Değişkenin tipi değişemez!
    mutable = true;
    
    // Gölgeleme ile değişkenlerin üzerine istenen tipte yazılabilir.
    let mutable = true;
}
```

### Ayrıca Bakın:

[`std` kütüphanesi][std], [`değişilebilirlik`][mut], [`çıkarım`][inference], ve [`gölgeleme`][shadowing]

[std]: https://doc.rust-lang.org/std/
[değişilebilirlik]: variable_bindings/mut.md
[çıkarım]: types/inference.md
[gölgeleme]: variable_bindings/scope.md
