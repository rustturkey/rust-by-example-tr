# Ifadeler

Bir Rust programı (çoğunlukla) bir dizi ifadelerden oluşur:

```rust,editable
fn main() {
    // ifade
    // ifade
    // ifade
}
```

Rust'ta birkaç tür ifade vardır. En yaygın ikisi değişken bağlayıcı bildirimi, ve bir ifade ile `;` kullanımıdır:

```rust,editable
fn main() {
    // değişken bağlayıcı
    let x = 5;

    // ifade;
    x;
    x + 1;
    15;
}
```

Bloklar da ifadelerdir, bu sebeple atamalarda değer olarak kullanılabilirler. Bloktaki son ifade, yerel bir değişken gibi yer ifadesine atanacaktır. Bununla birlikte, bloğun son ifadesi noktalı virgülle biterse, dönüş değeri `()` olacaktır.

```rust,editable
fn main() {
    let x = 5u32;

    let y = {
        let x_squared = x * x;
        let x_cube = x_squared * x;

        // Bu ifade `y` ye atanacaktır
        x_cube + x_squared + x
    };

    let z = {
        // Noktalı virgül bu ifadeyi önler(durdurur) ve `()` , `z` ye atanır
        2 * x;
    };

    println!("x is {:?}", x);
    println!("y is {:?}", y);
    println!("z is {:?}", z);
}
```
