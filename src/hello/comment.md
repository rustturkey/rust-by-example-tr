# Yorumlar

Tüm programlar yorum satırlarını kullanırlar, Rust birkaç farklı çeşitte yorum satırlarını destekler:

* Derleyici tarafından görmezden gelinen *standart yorumlar*: 
   * `// Satırın sonuna kadar süren satır yorumları`
   * `/* Sınırlayıcıya kadar süren blok halindeki yorumlar. */`
* *Doc(dokümantasyon) yorumları*  HTML kütüphanesiyle ayrıştırılır
  [dokümantasyon][docs]:
   * `/// Takip eden öğe için kütüphane belgeleri oluşturun.`
   * `//! Çevreleyen öğe için kütüphane belgeleri oluşturun.`

```rust,editable
fn main() {
    // Bu, satır yorumlarının bir örneğidir.
    // Satırın başında iki eğik çizgi var.
    // Ve burada yazılmış hiçbir şey derleyici tarafından okunmayacak

    // println!("Hello, world!");

    // Çalıştırın. Gördünüz mü? Now try deleting the two slashes, and run it again.

    /* 
     * Bu başka tip bir yorum, blok halinde yorum. Genel olarak,
     * satır yorumları tavsiye edilen yorum çeşididir. Ama
     * blok yorumlar kod parçalarını kısa süreli olarak devre dışı bırakmada son derece kullanışlıdır. /* Blok yorumlar /* iç içe olabilir, */ */
     * bu yüzden bu main() fonksiyonunda her şeyi yorumlamak için
     * sadece birkaç tuşa basmak yeterli. /*/*/* Deneyin! */*/*/
     */

    /*
    Not: Önceki `*` sütunu tamamen hoş gözükmesi içindi. Aslında o kadarına ihtiyacımız yok.
    */

    // Blok yorumları ile ifadeleri 
    // satır yorumlarından daha kolay değiştirebilirsiniz.
    // Sonucu değiştirmek için
    // Yorum sınırlayıcılarını silmeyi deneyin
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
}
```

### Ayrıca bakın:

[Kütüphane dokümantasyonu][docs]

[docs]: ../meta/doc.md
