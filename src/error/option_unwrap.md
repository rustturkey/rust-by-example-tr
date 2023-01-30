# `Option` & `unwrap`

Son örnekte, programı hataya teşvik edebileceğimizi gösterdik.
Programımıza eğer royal(kraliyet mensubu) uygun olmayan bir hediye alıysa - snake(yılan) `panic` yapmasını söyledik. Ama ya eğer royal bir hediye bekledi ve almadıysa? Bu da aynı derecede kötü olurdu, buna bir el atılması gerek!

Buna karşı  null string (`""`) testi yapa*biliriz* snake hediyesi için yaptığımız gibi.
Rust kullanırken, bunun yerine derleyicinin hediyenin olmadığı durumları göstermesini sağlayalım.

Bir yokluk olasılığı olduğunda, `std` kütüphanesindeki `Option<T>` isimli bir `enum` kullanılır. Kendisini iki "seçenek"ten biri olarak gösterir:

* `Some(T)`: `T` tipli bir öğe bulundu
* `None`: Öğe bulunamadı.

Bu vakalar, `match` yoluyla ya da örtülü olarak
`unwrap` yoluyla ele alınabilir. Örtülü ele alma ya içteki öğeyi döndürür ya da `panic`.

`panic`i [expect][expect] ile manuel olarak özelleştirmenin bir yolu olmadığını unutmayın,
ama `unwrap` aksi takdirde bizi açık ele almaya göre daha az anlamlı bir çıktıyla bırakır. Takip eden örnekte, açık ele alma istenirse `panic` seçeneğini korurken daha kontrollü bir sonuç verir.

```rust,editable,ignore,mdbook-runnable
// Sıradan olan her şeyi gördü ve her hediyeyi iyi bir şekilde değerlendirebilir.
// Tüm hediyeler açıkça `match` kullanılarak ele alınır.
fn give_commoner(gift: Option<&str>) {
    // Her durum için bir eylem planı belirleyin.
    match gift {
        Some("snake") => println!("Yuck! I'm putting this snake back in the forest."),
        Some(inner)   => println!("{}? How nice.", inner),
        None          => println!("No drink? Oh well."),
    }
}

// Korunaklı royal snake hediyelerini gördüğünde `panic` olacaktır.
// Tüm hediyeler açıkça `unwrap` kullanılarak ele alınır.
fn give_royal(gift: Option<&str>) {
    // `unwrap` `None` aldığında yani hiçbir şey almadığında `panic` döndürür.
    let inside = gift.unwrap();
    if inside == "snake" { panic!("AAAaaaaa!!!!"); }

    println!("I love {}s!!!!!", inside);
}

fn main() {
    let water  = Some("water");
    let lemonade = Some("lemonade");
    let void  = None;

    give_adult(water);
    give_adult(lemonade);
    give_adult(void);

    let coffee = Some("coffee");
    let nothing = None;

    drink(coffee);
    drink(nothing);
}
```

[expect]: https://doc.rust-lang.org/std/option/enum.Option.html#method.expect
