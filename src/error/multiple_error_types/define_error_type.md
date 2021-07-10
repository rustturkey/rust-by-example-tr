# Hata Tipini Tanımlamak

Bazen, tüm farklı hataların yerine tek bir hata tipini kullanarak temsil etmek(yani diğer hataları maskelemek) kodu basitleştirir. Bunu özel bir hatayla göstereceğiz.

Rust, kendi hata tiplerimizi tanımlamamızı sağlar. Genel olarak, "iyi" bir hata tipi:

* Farklı hataları aynı tiple temsil eder
* Kullanıcıya güzel, anlaşılabilir hata mesajları sunar
* Diğer tiplerle kıyaslanması kolaydır
    - İyi: `Err(EmptyVec)`
    - Kötü: `Err("Lütfen en az bir elemanlı bir vektör kullanın".to_owned())`
* Hata hakkında bilgi tutar
    - İyi: `Err(BadChar(c, position))`
    - Kötü: `Err("+ cannot be used here".to_owned())`
* Diğer hatalarla iyi uyum sağlar

```rust,editable
use std::fmt;

type Result<T> = std::result::Result<T, DoubleError>;

// Hata türlerimizi tanımlayalım. Bunlar, hata işleme durumlarımız için özelleştirilebilir.
// Artık, altta yatan bir hata uygulamasını erteleyebileceğimiz veya hata arasında 
// bir şey yapabileceğimiz kendi hatalarımızı yazabileceğiz
#[derive(Debug, Clone)]
struct DoubleError;

// Bir hatanın oluşturulması, görüntülenme biçiminden tamamen farklıdır.
// Karmaşık mantığın görüntü tarzıyla karıştırılması konusunda endişelenmenize gerek yok.
//
// Hatalar hakkında fazladan bilgi saklamadığımızı unutmayın. Bu, türlerimizi bu bilgiyi
// taşıyacak şekilde değiştirmeden hangi dizenin ayrıştırılamayacağını belirtemeyeceğimiz anlamına gelir.
impl fmt::Display for DoubleError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "invalid first item to double")
    }
}

fn double_first(vec: Vec<&str>) -> Result<i32> {
    vec.first()
        // Hatayı yeni tipe değiştirelim.
        .ok_or(DoubleError)
        .and_then(|s| {
            s.parse::<i32>()
                // Burada da yeni hata tipini güncelleyelim.
                .map_err(|_| DoubleError)
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
