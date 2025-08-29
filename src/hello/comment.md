# Yorumlar

Yazılan her program yorum gerektirir, Rust birkaç farklı yorum stilini destekler:

* Derleyici tarafından görmezden gelinen *alışılageldik yorumlar*:
   * `// Satır yorumları, satırın sonuna kadar sürecektir.`
   * `/* Blok yorumları sınırlayıcıya kadar sürecektir. */`
* *Doc yorumlar* yani dokümantasyon yorumları, HTML kütüphanesi dokümantasyonu tarafından ayrıştırılır:

  [dokümantasyon][docs]:
   * `/// Takip eden öğe için kütüphane dokümantasyonu oluştur.`
   * `//! Ek öğe için kütüphane dokümantasyonu oluştur.`

```rust,editable
fn main() {
    // Bu bir satır yorumudur
    // Satırın başında 2 bölü işaretiyle başlar
    // Ve derleyici tarafından burada yazılan hiçbir şey okunmayacaktır

    // println!("Merhaba, dünya!");

    // Çalıştırın, Gördünüz mü? Şimdi bir de o iki bölü işaretini silip yeniden çalıştırmayı deneyin.

    /* 
     * Bu da başka bir yorum şekli, blok yorum. Genel olarak,
     * Satır yorumları tavsiye edilen yorum şeklidir. Ama 
     * blok yorumlar geçici olarak kodun bir kısmını iptal etmek için oldukça kullanışlıdır. 
     * /* Blok yorumlar birleşik /* de olabilirler, */ */
     * bu sayede birkaç tuş vuruşuyla main() fonksiyonundaki
     * her şeyi yorum haline getirebilirsiniz. /*/*/* Haydi deneyin! */*/*/
     */

    /*
    Not: Önceki kolondaki `*` tamamen güzel görünüş içindi. 
    Gerçek anlamda ona ihtiyacımız yok. 
    */

    // İfadeler de satır yorumu yerine  rahatça blok yorumlar ile manipüle edilebilir. 
    // Sonucu değiştirmek için sınırlayıcıları silmeyi deneyin:
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
}

```

### Ayrıca bakın:

[Kütüphane dokümantasyonu][docs]

[docs]: ../meta/doc.md
