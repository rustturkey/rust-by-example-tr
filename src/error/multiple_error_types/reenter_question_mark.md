# `?`'nin Diğer Kullanımları

Önceki örnekte, `parse`(ayrıştırma) çağrısına anında tepkimizin bir kütüphane hatasından kaynaklanan hatayı bir boxed(kutulu) hataya `map`lemek(eşlemek) olduğuna dikkat edin:

```rust,ignore
.and_then(|s| s.parse::<i32>()
    .map_err(|e| e.into())
```

Bu basit ve yaygın bir işlem olduğundan, atlanması uygun olacaktır. Ne yazık ki `and_then` yeterince esnek olmadığından, bunu yapamaz. Ancak, yerine `?` kullanabiliriz.

`?` önceleri `unwrap` ya da `return Err(err)` olarak açıklanmıştı.
Bu çoğunlukla doğrudur. Aynı zamanda `unwrap` ya da
`return Err(From::from(err))` anlamına da gelir. `From::from` farklı tipler arasındabir dönüştürme aracı olduğundan bu `?` kullandığınız yerde hatanın dönüş tipine dönüştürülebildiği anlamına gelir, otomatik olarak dönüştürecektir.

Burada, `?` kullanarak önceki örneği yeniden yazıyoruz. Sonuç olarak, `map_err`, hata tipimiz için `From::from` implemente edildiğinde kaybolacak:

```rust,editable
use std::error;
use std::fmt;

// Takma adı `Box<dyn error::Error>`a değiştir.
type Result<T> = std::result::Result<T, Box<dyn error::Error>>;

#[derive(Debug)]
struct EmptyVec;

impl fmt::Display for EmptyVec {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "invalid first item to double")
    }
}

impl error::Error for EmptyVec {}

// Öncekiyle aynı yapı, ancak tüm `Results`(sonuçları) zincirlemek
// yerine `Options` yanına, `?` koyuyor, iç değeri hemen çıkarıyoruz.
fn double_first(vec: Vec<&str>) -> Result<i32> {
    let first = vec.first().ok_or(EmptyVec)?;
    let parsed = first.parse::<i32>()?;
    Ok(2 * parsed)
}

fn print(result: Result<i32>) {
    match result {
        Ok(n)  => println!("The first doubled is {}", n),
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

Bu aslında şu anda oldukça temiz. Orijinal `panic` ile kıyaslandığında, `unwrap` çağrılarıyla `?`nin yer değiştirmeye çok benzer, tabii dönüş tiplerinin `Result` olması dışında. Sonuç olarak, en üst düzeyde yıkımları(destruct) gerektirir.

### Ayrıca bakın:

[`From::from`][from] ve [`?`][q_mark]

[from]: https://doc.rust-lang.org/std/convert/trait.From.html
[q_mark]: https://doc.rust-lang.org/reference/expressions/operator-expr.html#the-question-mark-operator
