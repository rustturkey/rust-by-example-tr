# Deneme: linked-list(bağlı liste)

`enum`ların yaygın bir kullanımı bağlı liste oluşturmaktır:

```rust,editable
use crate::List::*;

enum List {
    // Cons: Bir öğeyi ve bir pointer'ı sonraki düğüme saran Tuple struct'ı
    Cons(u32, Box<List>),
    // Nil: Bağlı listenin sonunu belirten düğüm
    Nil,
}

// Metotlar bir enum'a eklenebilir
impl List {
    // Boş bir liste oluştur
    fn new() -> List {
        // `Nil`in tipi `List`
        Nil
    }

    // Bir listeyi yok edin, ardından aynı listeyi önünde yeni bir öğeyle döndürün 
    fn prepend(self, elem: u32) -> List {
        // `Cons`ın da tipi List
        Cons(elem, Box::new(self))
    }

    // Listenin uzunluğunu döndürün
    fn len(&self) -> u32 {
        // `self` eşlemelidir, çünkü bu metodun davranışı
        // `self` değişkenine bağlıdır
        // `self` `&List` tipine, ve `*self` `List` tipine sahiptir.
        // `&T` referansındaki eşleme yerine `T` somut tipi tercih edilir
        match *self {
            // Kuyruğun sahipliği alınamıyor, çünkü `self` ödünç alındı(borrow);
            // yerine kuyruğa yeni bir referans alınıyor:
            Cons(_, ref tail) => 1 + tail.len(),
            // Basit durum: Bir boş liste 0 uzunluğa sahiptir.
            Nil => 0
        }
    }

    // Listenin gösterimini (heap allocated(yığın ile ayrılmış)) string olarak döndürür
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!`, `print!`e benzer, ama konsola basmak yerine heap
                // allocated string döndürür
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // Boş bir bağlı liste oluştur
    let mut list = List::new();

    // Başa birkaç eleman ekle
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // Listenin son halini göster
    println!("linked list has length: {}", list.len());
    println!("{}", list.stringify());
}
```

### Ayrıca bakın:

[`Box`][box] ve [metotlar][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md
