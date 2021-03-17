# Enum'lar

`enum` anahtar kelimesi birkaç farklı çeşitten biri olabilen bir tipin oluşturulmasına izin verir. `struct` olarak geçerli olan herhangi bir değişken aynı zamanda `enum` değeri olarak da geçerlidir.

```rust,editable
// Bir web olayını sınıflandırmak için bir `enum` oluşturun. Her ikisinin de
// adlar ve tip bilgilerini birlikte belirttiğini unutmayın:
// `PageLoad != PageUnload` and `KeyPress(char) != Paste(String)`.
// Her biri bağımsızdır.
enum WebEvent {
    // Bir `enum`, `unit-like` (birim benzeri) olabilir,
    PageLoad,
    PageUnload,
    // tuple struct'ları(yapıları) gibi,
    KeyPress(char),
    Paste(String),
    // ya da c gibi yapılar.
    Click { x: i64, y: i64 },
}

// Bağımsız değişken olarak `WebEvent` enum'unu alan
//  ve hiçbir şey döndürmeyen(return) fonksiyon.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // `enum` içindeki `c` yıkımı .
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // `Click`in `x` ve `y`nin içinde yıkımı.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` bir string dilimine sahip olan bir `String` oluşturur.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## Tip takma adları(Type Aliases)

Bir tip takma adı kullanırsanız, her bir enum çeşidine kendisinin takmadı adı ile değinebilirsiniz.
Bu, enum'un adı çok uzun veya çok genelse ve siz onu yeniden adlandırmak istiyorsanız yararlı olabilir.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// Tip takma adı oluşturulur
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // Her çeşide uzun veya rahatsız edici şekilde değil, takma adıyla
    // değinebilirsiniz.
    let x = Operations::Add;
}
```

Bunu göreceğiniz en yaygın yer, `Self` takma adını kullanan `impl` bloklarıdır.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

Enum'lar ve tip takma adları hakkında daha fazla bilgi edinmek için, bu özelliğin Rust'ta stabilize edildiği andan itibaren oluşturulan
[stabilizasyon raporu][aliasreport]nu okuyabilirsiniz.

### Ayrıca bakın:

[`match`][match], [`fn`][fn], ve [`String`][str], ["İngilizce tip takma adı enum çeşitlilikleri" RFC'si][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
