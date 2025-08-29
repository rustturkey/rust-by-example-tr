# Formatlı Yazdırma

Yazdırma[`std::fmt`][fmt]'de tanımlanan bir dizi [`macro'lar`][macros] tarafından yönetilen bir işlemdir; bunlardan bazıları:

* `format!`: Biçimlendirilmiş metni [`String`][string] 'e yazar
* `print!`: `format!` ile aynıdır, ancak metin konsola  yazdırılır. (io::stdout).
* `println!`: `print!` ile aynıdır, ancak yeni bir satır eklenir.
* `eprint!`: `format!` ile aynıdır, ancak metin standart hataya yazdırılır. (io::stderr).
* `eprintln!`: `eprint!`ile aynıdır, ancak yeni bir satır eklenir.

Tüm metinler aynı şekilde ayrıştırılır. Rust, derleme zamanında biçimlendirme(formatlama) doğruluğunu kontrol eder.


```rust,editable,ignore,mdbook-runnable
fn main() {
    // Genel olarak, `{}` otomatik olarak herhangi bir
    // argümanla yer değiştirecektir. Bunlar dize(String)leştirilecektir.
    println!("{} gunler", 31);

    // Son ek olmadan 31, i32 olacaktır, 31'in türünü bir son ek ekleyerek
    // değiştirebilirsiniz. Örn. 31i64 sayısının türü i64'tür.

    // Bunun işe yaradığı çeşitli isteğe bağlı desenler vardır. 
    // Konumsal argümanlar kullanılabilir:
    println!("{0}, bu {1}. {1}, bu {0}", "Ali", "Veli");

    // Adlandırılmış argümanlar olarak da...
    println!("{subject} {verb} {object}",
             object="tembel kopek",
             subject="hizli kosan tilki",
             verb="ziplar");

    // Özel biçimlendirme `:` işaretinden sonra belirtilebilir.
    println!("{:b} kisiden {} tanesi binary(ikili) sistemi bilir, yarisi bilmez", 1, 2);

    // Metni belirtilen genişlikte sağa hizalayabilirsiniz. Bu takip eden çıktıyı verecektir:
    // "     1". 5 boşluk ve bir adet "1".
    println!("{number:>width$}", number=1, width=6);

    // Sayıları ekstra sıfırla doldurabilirsiniz. Bu "000001" çıktısını verecektir.
    println!("{number:>0width$}", number=1, width=6);

    // Rust doğru sayıda argümanın kullanıldığından emin olmak için de
    // kontrol edecektir.
    println!("Benim adim, {0}, {1} {0}", "Bond");
    // ÇÖZMELİSİNİZ! ^ Eksik argümanı ekleyin: "James"

    // `i32` içeren `Structure` isimli bir structure(yapı) oluşturun.
    #[allow(dead_code)]
    struct Structure(i32);

    // Ancak, bu yapı gibi özel tipler daha karmaşık bir işlem gerektirir.
    // örn. Bu bir işe yaramayacaktır:
    println!("Bu struct `{}` yazdirilmayacak...", Structure(3));
    // ÇÖZMELİSİNİZ! ^ Bu satırı yoruma alın.
}
```

[`std::fmt`][fmt] metnin görüntülenmesini yöneten birçok [`trait`][traits] yani nitelik içerir. 
Bunlardan ikisinin temel biçimi aşağıda listelenmiştir:

* `fmt::Debug`: `{:?}` işaretini kullanır. Hata ayıklama amacıyla metni biçimlendirir.
* `fmt::Display`: `{}` işaretini kullanır. Metni daha zarif ve kullanıcı dostu bir şekilde biçimlendirir.

Burada, std kütüphanesi bu türler için implementasyonlar sağladığından`fmt::Display` kullandık. Özel türlerde metin yazdırmak için daha fazla adım gerekecektir.

`fmt::Display` niteliğinin implemente edilmesi, otomatik olarak türünüzü [`String`][string] türüne [dönüştürme]mize olanak tanıyan [`ToString`] niteliğini de implemente eder.

### Etkinlikler

 * Yukarıdaki koddaki iki sorunu (bkz. ÇÖZMELİSİNİZ!) düzeltmek, böylece hatasız çalışacaklar.
 * Gösterilen ondalık basamaklı sayıyı kontrol ederek `Pi is roughly 3.142` yazdıran bir `println!` macro'su ekleyin. Bu alıştırmada, pi için tahmin olarak `let pi = 3.141592` kullanın. (İpucu: Görüntülenecek ondalık basamaklı sayıyı ayarlamak için [`std::fmt`][fmt] belgelerini kontrol edebilirsiniz.)

### Ayrıca bakın:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
ve [`traits`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
