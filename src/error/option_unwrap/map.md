# Combinators(Birleştiriciler): `map`

`match`, `Option`ları yönetmek için geçerli bir yöntem. Ancak, özellikle yalnızca bir girdiyle geçerli olan işlemler söz konusu olduğunda yoğun kullanımı sıkıcı bulabilirsiniz. Bu durumlarda, kontrol akışını modüler bir şekilde yönetmek için birleştiriciler([combinators][combinators]) kullanılabilir.
`Option`, `Some -> Some` `None -> None` haritalaması için `map()` isimli basit birleştirici metoda sahiptir. Çoklu `map()` çağrıları esneklik için zincirlenebilir.

Takip eden örnekte, `process()` sıkıştırılırken önceki tüm fonksiyonların yerine geçer.

```rust,editable
#![allow(dead_code)]

#[derive(Debug)] enum Food { Apple, Carrot, Potato }

#[derive(Debug)] struct Peeled(Food);
#[derive(Debug)] struct Chopped(Food);
#[derive(Debug)] struct Cooked(Food);

// Yiyecekleri soyma kısmı. Eğer hiçbir şey yoksa `None` döndürür.
// Aksi halde, soyulmuş yiyeceği döndürür.
fn peel(food: Option<Food>) -> Option<Peeled> {
    match food {
        Some(food) => Some(Peeled(food)),
        None       => None,
    }
}

// Yiyecekleri doğrama kısmı. Eğer hiçbir şey yoksa `None` döndürür.
// Aksi halde, doğranmış yiyeceği döndürür.
fn chop(peeled: Option<Peeled>) -> Option<Chopped> {
    match peeled {
        Some(Peeled(food)) => Some(Chopped(food)),
        None               => None,
    }
}

// Yiyecekleri pişirme kısmı. Burada durumu yönetmek için `match` yerine  `map()` kullanıyoruz.
fn cook(chopped: Option<Chopped>) -> Option<Cooked> {
    chopped.map(|Chopped(food)| Cooked(food))
}

// Yiyecekleri sırayla soyma, doğrama ve pişirme fonksiyonu.
// Kodu basitleştirmek için `map()`in birden fazla kullanımını zincirliyoruz. 
fn process(food: Option<Food>) -> Option<Cooked> {
    food.map(|f| Peeled(f))
        .map(|Peeled(f)| Chopped(f))
        .map(|Chopped(f)| Cooked(f))
}

// Yemeye çalışmadan önce yiyecek olup olmadığını kontrol edin.
fn eat(food: Option<Cooked>) {
    match food {
        Some(food) => println!("Mmm. {:?} güzeldi, sevdim.", food),
        None       => println!("Olamaz! Bu yenilebilir değil."),
    }
}

fn main() {
    let apple = Some(Food::Apple);
    let carrot = Some(Food::Carrot);
    let potato = None;

    let cooked_apple = cook(chop(peel(apple)));
    let cooked_carrot = cook(chop(peel(carrot)));
    // `Şimdi daha basit görünen process()`e bir bakış atalım .
    let cooked_potato = process(potato);

    eat(cooked_apple);
    eat(cooked_carrot);
    eat(cooked_potato);
}
```

### Ayrıca bakın:

[closures][closures], [`Option`][option], [`Option::map()`][map]

[combinators]: https://doc.rust-lang.org/reference/glossary.html#combinator
[closures]: ../../fn/closures.md
[option]: https://doc.rust-lang.org/std/option/enum.Option.html
[map]: https://doc.rust-lang.org/std/option/enum.Option.html#method.map
