# Fonksiyonlar

Fonksiyonlar `fn` anahtar sözcükleriyle bildirilirler. Argümanları değişkenlerdeki gibi tip açıklamalıdır, ve, fonksiyon bir değer döndürürse dönüş türü bir oktan sonra bildirilmelidir `->`.

Fonksiyonlardaki son ifade dönüş değeri olarak kullanılacaktır.
Alternatif olarak `return` ifadesi fonksiyonun içinden, döngülerin içinden ve hatta `if` ifadelerinden bile daha önce bir değer döndürmek için kullanılabilir.

Fonksiyonları kullanarak FizzBuzz(basit bir algoritma türü)'ı yeniden yazalım!

```rust,editable
// C/C++'taki gibi fonksiyon bildirim sırası diye bir kısıtlama yok!
fn main() {
    // Fonksiyonu burada kullanabiliriz, ve sonra bir yerde bildiririz.
    fizzbuzz_to(100);
}

// Boolean değer döndüren fonksiyon
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    // Köşe durumu, erken dönüş
    if rhs == 0 {
        return false;
    }

    // Bu bir ifade, `return` anahtar kelimesi burada gerekli değil
    lhs % rhs == 0
}

// Değer döndürmeyen fonksiyonlar,aslında birim tipini döndürürler `()`
fn fizzbuzz(n: u32) -> () {
    if is_divisible_by(n, 15) {
        println!("fizzbuzz");
    } else if is_divisible_by(n, 3) {
        println!("fizz");
    } else if is_divisible_by(n, 5) {
        println!("buzz");
    } else {
        println!("{}", n);
    }
}

// Fonksiyon `()` döndürdüğünde, dönüş tipi imzadan çıkartılabilir
fn fizzbuzz_to(n: u32) {
    for n in 1..=n {
        fizzbuzz(n);
    }
}
```
