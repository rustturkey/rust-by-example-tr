# `Result`

[`Result`][result], [`Option`][option] tipinin olası *yokluk* yerine hatayı açıklayan daha zengin versiyonudur.

Yani, `Result<T, E>` iki sonuçtan birine sahip olabilir:

* `Ok(T)`: `T` öğesi bulundu.
* `Err(E)`:  `E` öğesi ile ilgili bir hata bulundu.

Geleneksel olarak, beklenen sonuç `Ok` iken beklenmedik sonuç `Err`'dir.

`Option` gibi, `Result`'ın da kendisiyle ilişkili birçok metodu vardır. Örneğin `unwrap()`, ya `T` öğesini ya da `panic`'i oluşturur. Durum ele alma işlemi için `Result` ve `Option` örtüşen birçok birleştirici vardır.

Rust ile çalışırken, [`parse()`][parse] metodu gibi
`Result` türünü döndüren metotlarla karşılaşmanız pek mümkündür. Bir string'i diğer bir türe ayrıştırmak her zaman mümkün olmayabilir, bu nedenle `parse()` olası başarısızlığı gösteren bir
`Result` döndürür.

Hadi başarılı ve başarısız şekilde `parse()` metoduna bakalım:

```rust,editable,ignore,mdbook-runnable
fn multiply(first_number_str: &str, second_number_str: &str) -> i32 {
    // Let's try using `unwrap()` to get the number out. Will it bite us?
    let first_number = first_number_str.parse::<i32>().unwrap();
    let second_number = second_number_str.parse::<i32>().unwrap();
    first_number * second_number
}

fn main() {
    let twenty = multiply("10", "2");
    println!("double is {}", twenty);

    let tt = multiply("t", "2");
    println!("double is {}", tt);
}
```

Başarısız durumda, `parse()`,  `unwrap()` metodunun `panic` çağırmaması için bizi bir hatayla bırakır. Ek olarak, `panic` programımızdan çıkar ve hoş olmayan bir hata mesajı verir.

Hata mesajımızın kalitesini artırmak için, dönüş türü hakkında daha spesifik olmalı ve hatayı açıkça ele almalıyız.

## `Result`'ı `main` içinde kullanmak

`Result` türü, açıkça belirtilmişse `main`'in dönüş türü de olabilir. Tipik olarak `main` şu biçimde olacaktır:

```rust
fn main() {
    println!("Hello World!");
}
```

Bununla birlikte, `main`, bir `Result` türüne de sahip olabilir. Eğer bir hata oluşursa, `main` fonksiyonunun içinde bir hata kodu oluşturur ve hatanın debug temsilini yazdırır.
([`Debug`] niteliğini kullanarak). Takip eden örnekte, böyle bir senaryoyu gösterir ve [takip eden bölümde] ele alınan hususlara değinir.

```rust,editable
use std::num::ParseIntError;

fn main() -> Result<(), ParseIntError> {
    let number_str = "10";
    let number = match number_str.parse::<i32>() {
        Ok(number)  => number,
        Err(e) => return Err(e),
    };
    println!("{}", number);
    Ok(())
}
```


[option]: https://doc.rust-lang.org/std/option/enum.Option.html
[result]: https://doc.rust-lang.org/std/result/enum.Result.html
[parse]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`Debug`]: https://doc.rust-lang.org/std/fmt/trait.Debug.html
[takip eden bölümde]: result/early_returns.md
