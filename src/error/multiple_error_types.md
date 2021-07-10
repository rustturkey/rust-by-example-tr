# Çoklu Hata Tipleri

Önceki örnekler oldukça rahattı; Bir `Result`ın bir başka `Result` ile etkileşimi ve bir `Option`ın başka bir `Option` ile etkileşimi gibiydi.

Bazen bir `Option` diğer bir `Result` ile etkileşim kurmak zorundadır, ya da
`Result<T, Error1>`, `Result<T, Error2>` ile. Tüm bu durumlarda, farklı hata türlerimizi, birleştirilebilir ve etkileşimi kolay hale getirecek şekilde yönetmek istiyoruz. 

Takip eden örnekte, iki `unwrap` örneği farklı hata tipleri oluşturur. `parse::<i32>` bir
`Result<i32, ParseIntError>` döndürürken,`Vec::first` bir `Option` döndürür:

```rust,editable,ignore,mdbook-runnable
fn double_first(vec: Vec<&str>) -> i32 {
    let first = vec.first().unwrap(); // error 1'i oluşturur
    2 * first.parse::<i32>().unwrap() // error 2'yi oluşturur
}

fn main() {
    let numbers = vec!["42", "93", "18"];
    let empty = vec![];
    let strings = vec!["tofu", "93", "18"];

    println!("The first doubled is {}", double_first(numbers));

    println!("The first doubled is {}", double_first(empty));
    // Error 1: girdi vector'ü boş

    println!("The first doubled is {}", double_first(strings));
    // Error 2: öğe sayıya ayrıştırılamaz
}
```

İlerleyen bölümlerde, bu tip problemler için birkaç stratejileri ele alacağız.
