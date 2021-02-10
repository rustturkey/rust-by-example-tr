# Özellikler

Bir özellik, bazı modüllere, crate(sandık)'e veya öğeye uygulanan meta(üst) veridir. Bu metadata(üst veri)
şunlar için kullanılır:

<!-- TODO: Link these to their respective examples -->

* [koşullu kod derlenmesi][cfg]
* [crate adını, sürümünü ve tipini (ikili veya kütüphane)][crate]
* [lintleri] devre dışı bırak [lint]  (uyarılar)
* derleyici özelliklerini etkinleştir (macro'lar, glob içe aktarımlar vb.)
* yabancı bir kütüphaneye bağlantı
* fonksiyonları unit(birim) testi olarak işaretleme
* fonksiyonları bir karşılaştırmanın parçası olarak işaretleme

Özellikler bütün bir crate'e başvurduğunda, söz dizimi `#![crate_attribute]`,
ve bir modül veya öğeye başvurduğunda, söz dizimi `#[item_attribute]`
(eksiğin farkına varın `!`).

Özellikler farklı söz dizimleriyle argümanlar da alabilirler:

* `#[attribute = "deger"]`
* `#[attribute(key = "deger")]`
* `#[attribute(deger)]`

Özellikler çoklu değer alabilir ve çoklu satırla ayrılabilirler de:

```rust,ignore
#[attribute(deger, deger2)]


#[attribute(deger, deger2, deger3,
            deger4, deger5)]
```

[cfg]: attribute/cfg.md
[crate]: attribute/crate.md
[lint]: https://en.wikipedia.org/wiki/Lint_%28software%29
