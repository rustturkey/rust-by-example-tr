# Genelleyiciler

*Generic'ler (Genelleyiciler)* tipleri ve fonksiyonları daha geniş durumlara genelleme konusudur. Bu, birçok yönden kod yinelemesini azaltmak için oldukça kullanışlıdır, ancak daha çok söz dizimi(syntax) kullanımı gerektirebilir. Yani, generic olmak; genel bir tipin hangi tipler üzerinde geçerli kabul edildiğini belirtmek için büyük özen gerektirir. Generic'lerin en basit ve en yaygın kullanımı tip parametreleri içindir.

Bir tip parametresi, açılı ayraçlar ve büyük harfli
[camel case][camelcase] kullanılarak belirtilir: `<Aaa, Bbb, ...>`. "Generic tip parametreleri" genellikle şu şekilde temsil edilir: `<T>`. Rust'ta "generic", bir veya daha fazla generic tip parametresini `<T>` kabul eden her şeyi tanımlar. Generic bir tip parametresi olarak belirtilen herhangi bir tip generic yani geneldir ve diğer her şey somuttur(generic olmayan).

Örneğin, herhangi bir tipten bağımsız `foo` isimli `T` bağımsız tipte argüman alan *generic fonksiyon* tanımlamak:

```rust,ignore
fn foo<T>(arg: T) { ... }
```

Çünkü `T` `<T>` kullanılarak genel bir tip parametresi olarak bildirildiğinden, burada `(arg: T)` olarak kullanıldığında generic kabul edilir. `T` daha önce `struct` olarak tanımlanmış olsa bile geçerli olan budur.

Bu örnek bazı söz dizimlerini gösterir:

```rust,editable
// Somut tip `A`.
struct A;

// `Single` tipini tanımlarken, `A`nın ilk kullanımından önce `<A>` gelmez.
// Bu nedenle, `Single` bir somut tiptir, ve `A` yukarıdaki gibi tanımlanır.
struct Single(A);
//            ^ `Single`ın `A` tipinin ilk kullanımı.

// Burada, `<T>`, `T`nin ilk kullanımından önce gelir, bu sebeple `SingleGen` generic bir tiptir.
// `T` tip parametresi generic olduğundan, herhangi bir şey olabilir;
// tepede tanımalanan somut `A` tipi de.
struct SingleGen<T>(T);

fn main() {
    // `Single` somuttur ve açıkça `A` alır.
    let _s = Single(A);
    
    // Tipi `SingleGen<char>` olan `_char` değişken tanımlayın
    // ve `SingleGen('a')` değerini verin.
    // Burada, `SingleGen` açıkça belirtilmiş bir tip parametresine sahiptir.
    let _char: SingleGen<char> = SingleGen('a');

    // `SingleGen` ayrıca dolaylı olarak belirtilen bir tip parametresine sahip olabilir:
    let _t    = SingleGen(A); // Tepe tanımlanan `A`yı kullanır.
    let _i32  = SingleGen(6); // `i32`yi kullanır.
    let _char = SingleGen('a'); // `char`ı kullanır.
}
```

### Ayrıca Bakınız:

[`structs`][structs]

[structs]: custom_types/structs.md
[camelcase]: https://en.wikipedia.org/wiki/CamelCase
