# `Box`ing Hataları

Orijinal hataları korurken basit kod yazmanın bir yolu onları [`Box`][box]'lamaktır.  Dezavantajı, temel alınan hata türünün yalnızca çalışma zamanında bilinmesi ve [statik olarak belirlenmemesidir][dynamic_dispatch].

stdlib, Box'ın [`From`][from] aracılığıyla `Error` niteliğini uygulayan herhangi bir türden `Box<Error>` nitelik nesnesine dönüştürme implementesini sağlayarak hatalarımızı Box'lamaya yardımcı olur.

```rust,editable
use std::error;
use std::fmt;

// Takma adı `Box<error::Error>` olarak değiştirin.
type Result<T> = std::result::Result<T, Box<dyn error::Error>>;

#[derive(Debug, Clone)]
struct EmptyVec;

impl fmt::Display for EmptyVec {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "invalid first item to double")
    }
}

impl error::Error for EmptyVec {}

fn double_first(vec: Vec<&str>) -> Result<i32> {
    vec.first()
        .ok_or_else(|| EmptyVec.into()) // Converts to Box
        .and_then(|s| {
            s.parse::<i32>()
                .map_err(|e| e.into()) // Converts to Box
                .map(|i| 2 * i)
        })
}

fn print(result: Result<i32>) {
    match result {
        Ok(n) => println!("The first doubled is {}", n),
        Err(e) => println!("Error: {}", e),
    }
}

fn main() {
    let numbers = vec!["42", "93", "18"];
    let empty = vec![];
    let strings = vec!["tofu", "93", "18"];

    print(double_first(numbers));
    print(double_first(empty));
    print(double_first(strings));
}
```

### Ayrıca bakın:

[Dinamik dağıtım][dynamic_dispatch] ve [`Error` niteliği][error]

[box]: https://doc.rust-lang.org/std/boxed/struct.Box.html
[dynamic_dispatch]: https://doc.rust-lang.org/book/ch17-02-trait-objects.html#trait-objects-perform-dynamic-dispatch
[error]: https://doc.rust-lang.org/std/error/trait.Error.html
[from]: https://doc.rust-lang.org/std/convert/trait.From.html
