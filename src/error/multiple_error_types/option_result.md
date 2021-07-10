# `Result`(Sonuç)'ları `Option`(Seçenek)'ların dışına çekmek

Karışık hata tiplerini ele almanın en basit yolu, onları birbirine gömmektir.

```rust,editable
use std::num::ParseIntError;

fn double_first(vec: Vec<&str>) -> Option<Result<i32, ParseIntError>> {
    vec.first().map(|first| {
        first.parse::<i32>().map(|n| 2 * n)
    })
}

fn main() {
    let numbers = vec!["42", "93", "18"];
    let empty = vec![];
    let strings = vec!["tofu", "93", "18"];

    println!("The first doubled is {:?}", double_first(numbers));

    println!("The first doubled is {:?}", double_first(empty));
    // Hata 1: girdi vektörü boş

    println!("The first doubled is {:?}", double_first(strings));
    // Hata 2: öge bir sayıya ayrıştırılamıyor
}
```

Hataların üzerinde işlem yapmayı durdurmak isteyeceğimiz zamanlar vardır ([`?`][enter_question_mark] ile gibi) ama `Option` `None`(hiçbiri) olduğunda olduğu gibi devam edin. `Result` ve `Option`'ı değiştirmek için birkaç combinator(birleştirici) kullanışlıdır.

```rust,editable
use std::num::ParseIntError;

fn double_first(vec: Vec<&str>) -> Result<Option<i32>, ParseIntError> {
    let opt = vec.first().map(|first| {
        first.parse::<i32>().map(|n| 2 * n)
    });

    opt.map_or(Ok(None), |r| r.map(Some))
}

fn main() {
    let numbers = vec!["42", "93", "18"];
    let empty = vec![];
    let strings = vec!["tofu", "93", "18"];

    println!("The first doubled is {:?}", double_first(numbers));
    println!("The first doubled is {:?}", double_first(empty));
    println!("The first doubled is {:?}", double_first(strings));
}
```

[enter_question_mark]: ../result/enter_question_mark.md
