# To and from Strings(Katarlara ve Katarlardan)

## String(Katar)'e Dönüşüm

Herhangi bir tipi `String`e dönüştürmek gayet basit bir şekilde [`ToString`] niteliğini o tip için implemente etmektir.
Ama bunu doğrudan yapmak yerine, otomatik olarak [`ToString`] sağlayan ve aynı zamanda [`print!`][print] bölümünde de anlatıldığı gibi tipi yazdırmaya izin veren [`fmt::Display`][Display] niteliğini uygulamalısınız. 

```rust,editable
use std::fmt;

struct Circle {
    radius: i32
}

impl fmt::Display for Circle {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Circle of radius {}", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```

## String'leri Ayrıştırmak

Bir string'i dönüştürmek için en sık kullanılan tiplerden biri sayılardır. Bunun deyimsel yaklaşımı; [`parse`] fonksiyonunu kullanmak, tip çıkarımını düzenlemek veya 'turbofish' söz dizimini kullanarak ayrıştırılacak tipi belirlemektir.
Her iki alternatif de aşağıdaki örnekte gösterilmektedir.

Bu, [`FromStr`] niteliği bu tip için implemente edildiği sürece string'i belirtilen tipe dönüştürecektir.
Standart kütüphane içindeki çeşitli tipler için implemente edilir. Bu fonksiyonelliği kullanıcı tanımlı bir tip üzerinde elde etmek için, bu tip üzerinde [`FromStr`] niteliğini implemente etmeniz yeterlidir.

```rust,editable
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let sum = parsed + turbo_parsed;
    println!("Sum: {:?}", sum);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html
