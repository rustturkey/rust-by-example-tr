# Variable Bindings
Rust sabit(statik) yazım tekniği ile tip güvenliği sağlar. Değişken bağlamaları, tanımlandığında tip açıklaması içerebilir. 
Bununla birlikte, çoğu durumda, derleyici
değişkenin tipini bağlamdan çıkarabilir ve bu ek açıklama yükünü büyük ölçüde azaltır.

Değerler(değiştirilemeyen değerler gibi), `let` bağlama bildiricisi kullanılarak değişkenlere bağlanabilir.

```rust,editable
fn main() {
    let an_integer = 1u32;
    let a_boolean = true;
    let unit = ();

    // `an_integer` değişkenini `copied_integer` değişkenine kopyalamak
    let copied_integer = an_integer;

    println!("Bir tamsayi(integer): {:?}", copied_integer);
    println!("Bir mantiksal degisken(boolean): {:?}", a_boolean);
    println!("Birim degerle tanisin: {:?}", unit);

    // Derleyici, kullanılmayan değişken bağlamları konusunda uyarır
    // bu uyarılar değişkenin adının önüne bir alt çizgi koyarak susturulabilir
    let _unused_variable = 3u32;

    let noisy_unused_variable = 2u32;
    // FIXME ^Uyarıyı bastırmak için alt çizgi içeren bir örnek
}
```
