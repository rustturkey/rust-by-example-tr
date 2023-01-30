# C gibi

`enum`'lar C gibi de kullanılabilirler.

```rust,editable
// Kullanılmayan kod için verilen uyarıları gizleyen özellik.
#![allow(dead_code)]

// dahili ayırıcı ile enum (0'da başlar)
enum Number {
    Zero,
    One,
    Two,
}

// aleni ayırıcı ile enum 
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    // `enums` integer(tam sayılar) gibi de dökümlenebilir, kullanılabilirler.
    println!("zero is {}", Number::Zero as i32);
    println!("one is {}", Number::One as i32);

    println!("roses are #{:06x}", Color::Red as i32);
    println!("violets are #{:06x}", Color::Blue as i32);
}
```

### Ayrıca bakın:

[Dökümleme(Cast)][cast]

[cast]: ../../types/cast.md
