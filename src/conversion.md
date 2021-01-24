# Dönüşüm

Temel tipler, [döküm] yoluyla birbirine dönüştürülebilir.

Rust [nitelik]'leri kullanarak özel tipler(yani `struct` ve `enum`) arasındaki dönüşümü ele alır. Genel dönüşümler, [`From`] ve [`Into`] niteliklerini kullancaktır. Bununla birlikte, daha yaygın durumlar için, özellikle `String`(dizeler)(katarlar)dan veya dizelere dönüşüm yapılırken daha spesifik olanları vardır.

[döküm]: types/cast.md
[nitelik]: trait.md
[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
