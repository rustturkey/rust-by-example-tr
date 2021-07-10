# Wrapping(Açma) Hataları

Boxing hatalarına bir alternatif, onları kendi hata tipinize wrap etmek(sarmaktır).

```rust,editable
use std::error;
use std::error::Error as _;
use std::num::ParseIntError;
use std::fmt;

type Result<T> = std::result::Result<T, DoubleError>;

#[derive(Debug)]
enum DoubleError {
    EmptyVec,
    // Hatalar için parse(ayrıştırma) hatası uygulamasını erteleyeceğiz
    // Ek bilgi sağlamak, tipe daha fazla veri eklemeyi gerektirir.
    Parse(ParseIntError),
}

impl fmt::Display for DoubleError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        match *self {
            DoubleError::EmptyVec =>
                write!(f, "please use a vector with at least one element"),
            // Wrapped(sarılmış) hata ek bilgiler içerir ve source() metoduyla 
            // source() metoduyla kullanılabilir.
            DoubleError::Parse(..) =>
                write!(f, "the provided string could not be parsed as int"),
        }
    }
}

impl error::Error for DoubleError {
    fn source(&self) -> Option<&(dyn error::Error + 'static)> {
        match *self {
            DoubleError::EmptyVec => None,
            // Nedeni, temeldeki implemente hatası tipidir. 
            // Dolaylı olarak `&error::Error` nitelik nesnesine cast edin(yayın). 
            // Bu çalışacaktır çünkü temel tip zaten `Error` niteliğini implemente eder.
            DoubleError::Parse(ref e) => Some(e),
        }
    }
}

// `ParseIntError`dan `DoubleError`a dönüşümü implemente edin.
// Bu otomatik olarak `?` ile çağrılacaktır. `ParseIntError` ise
// `DoubleError` dönüştürülmelidir.
impl From<ParseIntError> for DoubleError {
    fn from(err: ParseIntError) -> DoubleError {
        DoubleError::Parse(err)
    }
}

fn double_first(vec: Vec<&str>) -> Result<i32> {
    let first = vec.first().ok_or(DoubleError::EmptyVec)?;
    // Burada bir `DoubleError` oluşturmak için örtülü olarak `From`'un 
    // `ParseIntError` implementesini kullanıyoruz (yukarıda tanımladığımız).
    let parsed = first.parse::<i32>()?;

    Ok(2 * parsed)
}

fn print(result: Result<i32>) {
    match result {
        Ok(n)  => println!("The first doubled is {}", n),
        Err(e) => {
            println!("Error: {}", e);
            if let Some(source) = e.source() {
                println!("  Caused by: {}", source);
            }
        },
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

Bu, hataların ele alınması için biraz daha fazla standart ekler ve tüm uygulamalarda gerekli olmayabilir. Sizin için basmakalıpları halledebilecek kütüphaneler var.

### Ayrıca bakın:

[`From::from`][from] ve [`Enums`][enums]

[from]: https://doc.rust-lang.org/std/convert/trait.From.html
[enums]: ../../custom_types/enum.md
