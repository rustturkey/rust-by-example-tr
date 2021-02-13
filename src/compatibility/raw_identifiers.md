# Ham Tanımlayıcılar

Rust, birçok programlama dilinde olduğu gibi "keywords" yani "anahtar kelimeler" konseptini içerir.
Bu tanımlayıcılar dil için bir şeyler ifade eder, bu nedenle onları değişken adı, fonksiyon adı ve bunlar gibi yerlerde kullanamazsınız. Ham tanımlayıcılar normalde izin verilmediği yerlerde bu anahtar kelimeleri kullanabilmenize izin verir.
Bu, özellikle; Rust yeni anahtar kelimeler sunduğunda ve Rust'ın eski bir sürümünü kullanan bir kütüphane, daha yeni bir sürümde tanıtılan bir anahtar kelimelerle aynı ada sahip bir değişken veya fonksiyona sahip olduğunda çok yararlıdır.

Örneğin, `try` isimli bir fonksiyonu dışa aktaran `foo` isimli  bir crate'in 2015 versiyon Rust ile derlendiğini düşünün. Bu anahtar kelime 2018 sürümündeki yeni bir özellik için ayrılmıştır, bu nedenle ham tanımlayıcılar olmasaydı bu fonksiyonu adlandırmanın bir yolu olmazdı.

```rust,ignore
extern crate foo;

fn main() {
    foo::try();
}
```

Şu hatayı alırdınız:

```text
error: expected identifier, found keyword `try`
 --> src/main.rs:4:4
  |
4 | foo::try();
  |      ^^^ expected identifier, found keyword
```

Ama aynı kodu ham tanımlayıcıyla yazabilirsiniz:

```rust,ignore
extern crate foo;

fn main() {
    foo::r#try();
}
```
