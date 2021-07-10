# `panic`

Göreceğimiz en basit hata işleme mekanızması `panic`tir. Bir hata mesajı yazdırır, yığını çözmeye başlar ve genellikle programı sonlandırır.
Aşağıda, hata koşulumuzda açıkça `panic`i çağırıyoruz :

```rust,editable,ignore,mdbook-runnable
fn drink(beverage: &str) {
    // You shouldn't drink too much sugary beverages.
    if beverage == "lemonade" { panic!("AAAaaaaa!!!!"); }

    println!("Some refreshing {} is all I need.", beverage);
}

fn main() {
    drink("water");
    drink("lemonade");
}
```
