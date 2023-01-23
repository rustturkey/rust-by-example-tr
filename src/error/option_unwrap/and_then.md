# Combinators (Birleştiriciler): `and_then`

`map()`, `match` ifadelerini basitleştirmenin zincirlenebilir bir yolu olarak tanımlanır. 
Ancak, `Option<T>` döndüren bir fonksiyonda `map()` kullanımı 
iç içe geçmiş `Option<Option<T>>` ile sonlanır. Birden çok çağrıyı birlikte zincirlemek kafa karıştırıcı olabilir. Tam burada, bazı dillerde "flatmap" olarak bilinen `and_then()` adlı başka bir birleştirici devreye girer. 

`and_then()` paketlenmiş değer ile fonksiyon girdisini çağırır ve sonucu döndürür. Eğer `Option` değeri `None` ise, onun yerine `None` değerini döndürür.

Takip eden örnekte, `cookable_v2()`, `Option<Food>` ile sonuçlanır. 
`and_then()` yerine `map()` kullanımı `eat()`için geçersiz bir tip olan `Option<Option<Food>>` sonucunu verecektir.

```rust,editable
#![allow(dead_code)]

#[derive(Debug)] enum Food { CordonBleu, Steak, Sushi }
#[derive(Debug)] enum Day { Monday, Tuesday, Wednesday }

// Sushi için gereken malzemelerimiz yok.
fn have_ingredients(food: Food) -> Option<Food> {
    match food {
        Food::Sushi => None,
        _           => Some(food),
    }
}

//Cordon Bleu hariç her şeyin tarifi var.
fn have_recipe(food: Food) -> Option<Food> {
    match food {
        Food::CordonBleu => None,
        _                => Some(food),
    }
}

// Bir yemeği yapabilmek için hem tarifine hem de gerektirdiği malzemelere sahip olmalıyız.
// Bu mantığı bir `match `zinciriyle temsil edebiliriz:
fn cookable_v1(food: Food) -> Option<Food> {
    match have_recipe(food) {
        None       => None,
        Some(food) => match have_ingredients(food) {
            None       => None,
            Some(food) => Some(food),
        },
    }
}

// Bu, `and_then()` ile rahatlıkla yeniden yazılabilir:
fn cookable_v2(food: Food) -> Option<Food> {
    have_recipe(food).and_then(have_ingredients)
}

fn eat(food: Food, day: Day) {
    match cookable_v2(food) {
        Some(food) => println!("Yay! On {:?} we get to eat {:?}.", day, food),
        None       => println!("Oh no. We don't get to eat on {:?}?", day),
    }
}

fn main() {
    let (cordon_bleu, steak, sushi) = (Food::CordonBleu, Food::Steak, Food::Sushi);

    eat(cordon_bleu, Day::Monday);
    eat(steak, Day::Tuesday);
    eat(sushi, Day::Wednesday);
}
```

### Ayrıca bakınız:

[closures][closures], [`Option`][option], and [`Option::and_then()`][and_then]

[closures]: ../../fn/closures.md
[option]: https://doc.rust-lang.org/std/option/enum.Option.html
[and_then]: https://doc.rust-lang.org/std/option/enum.Option.html#method.and_then
