# `Result`s(Sonuçlar) Üzerine Yineleme

Bir `Iter::map` işlemi başarısız olabilir, örneğin:

```rust,editable
fn main() {
    let strings = vec!["tofu", "93", "18"];
    let numbers: Vec<_> = strings
        .into_iter()
        .map(|s| s.parse::<i32>())
        .collect();
    println!("Results: {:?}", numbers);
}
```

Bununla başa çıkmak için strateji adımlarına geçelim.

## `filter_map()` ile Başarısız(fail) Öğeleri Yok Saymak

`filter_map` bir fonksiyon çağırır ve sonuçları `None`(yok) olanları filtreler.

```rust,editable
fn main() {
    let strings = vec!["tofu", "93", "18"];
    let numbers: Vec<_> = strings
        .into_iter()
        .filter_map(|s| s.parse::<i32>().ok())
        .collect();
    println!("Results: {:?}", numbers);
}
```

## `collect()` ile Tüm Başarısız İşlemler

`Result` sonucu (`Result<Vec<T>, E>`) gibi sonuç vektörüne dönüştürülebilen (`Vec<Result<T, E>>`) olan `FromIter`i implemente eder. Bir `Result::Err` bulunduğunda, yineleme sona erecektir.

```rust,editable
fn main() {
    let strings = vec!["tofu", "93", "18"];
    let numbers: Result<Vec<_>, _> = strings
        .into_iter()
        .map(|s| s.parse::<i32>())
        .collect();
    println!("Results: {:?}", numbers);
}
```

Bu teknik `Option` ile de kullanılabilir.

## `partition()` ile Tüm Geçerli(Valid) Değerleri ve Hataları Toplayın 
 
```rust,editable
fn main() {
    let strings = vec!["tofu", "93", "18"];
    let (numbers, errors): (Vec<_>, Vec<_>) = strings
        .into_iter()
        .map(|s| s.parse::<i32>())
        .partition(Result::is_ok);
    println!("Numbers: {:?}", numbers);
    println!("Errors: {:?}", errors);
}
```

Sonuçlara baktığınızda, her şeyin hala `Result` bölümünde olduğunu fark edeceksiniz. Bunun için biraz daha standart şablona ihtiyaç var.

```rust,editable
fn main() {
    let strings = vec!["tofu", "93", "18"];
    let (numbers, errors): (Vec<_>, Vec<_>) = strings
        .into_iter()
        .map(|s| s.parse::<i32>())
        .partition(Result::is_ok);
    let numbers: Vec<_> = numbers.into_iter().map(Result::unwrap).collect();
    let errors: Vec<_> = errors.into_iter().map(Result::unwrap_err).collect();
    println!("Numbers: {:?}", numbers);
    println!("Errors: {:?}", errors);
}
```
