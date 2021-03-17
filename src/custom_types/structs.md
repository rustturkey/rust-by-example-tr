# Structure'lar (Yapılar)

Structure'ların üç farklı tipi ("structs")
`struct` anahtar kelimesini kullanarak oluşturulabilir:

* Tuple struct'lar, yani temelde, tuple olarak isimlendirilen yapılar.
* Klasik[C struct'ları][c_struct]
* Unit(birim) struct'lar, yani üyesiz olanlar, genelleyiciler için kullanışlıdır.

```rust,editable
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// Bir unit struct
struct Unit;

// Bir tuple struct
struct Pair(i32, f32);

// İki üyesi olan bir struct
struct Point {
    x: f32,
    y: f32,
}

// Struct'lar başka bir struct'ın üyeleri olarak yeniden kullanılabilir
#[allow(dead_code)]
struct Rectangle {
    // Sol üst ve sağ alt köşelerin boşlukta olduğu yere göre 
    // bir dikdörtgen belirtilebilir.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // Kısa gösterimle üye içeren bir struct oluşturur
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // Hata ayıklaması struct'ını yazdırır
    println!("{:?}", peter);


    // `Point` örneklendirmesi
    let point: Point = Point { x: 10.3, y: 0.4 };

    // point'in üyelerine erişim
    println!("point coordinates: ({}, {})", point.x, point.y);

    // Diğer struct'ın üyelerini kullanmak için struct güncelleme söz dizimini kullanarak yeni bir point yaratır
    let bottom_right = Point { x: 5.2, ..point };

    // `bottom_right.y`, `point.y`  ile aynı olacaktır çünkü
    // `point`ten üye kullandık
    println!("second point: ({}, {})", bottom_right.x, bottom_right.y);

    // `let` bağlamıyla point yok edildi(yıkım/destructure)
    let Point { x: top_edge, y: left_edge } = point;

    let _rectangle = Rectangle {
        // struct örneklendirmesi ifadesi
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // unit struct örneklendirmesi ifadesi
    let _unit = Unit;

    //  tuple struct örneklendirmesi ifadesi
    let pair = Pair(1, 0.1);

    // tuple struct'ın üyelerine erişim
    println!("pair contains {:?} and {:?}", pair.0, pair.1);

    // tuple struct'ın yıkımı
    let Pair(integer, decimal) = pair;

    println!("pair contains {:?} and {:?}", integer, decimal);
}
```

### Faaliyet

1. Bir dikdörtgenin alanını hesaplayan `rect_area` fonksiyonunu ekleyin (iç içe yıkmayı kullanmayı deneyin).
2. `Point` ve bir `f32`yi değişken olarak alan `square` fonksiyonunu ekleyin, sol alt köşesi noktada, genişliği ve yüksekliği `f32`ye karşılık gelen bir `Rectangle` (Dikdörtgen) döndürür.

### Ayrıca bakın

[`özellikler`][attributes], ve [yıkım][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md
