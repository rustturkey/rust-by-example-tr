# use

`use` bildirimi kullanıldığında elle kapsam belirlemeye gerek yoktur:

```rust,editable
// Kullanılmayan kod için verilen uyarıları gizleyen özellik.
#![allow(dead_code)]

enum Status {
    Rich,
    Poor,
}

enum Work {
    Civilian,
    Soldier,
}

fn main() {
    // Aleni `use` bildirimi elle kapsam belirleme olmadan 
    // kullanılabilmelerini sağlar.
    use crate::Status::{Poor, Rich};
    // Otomatik olarak `Work`ün içindeki her isim `use`lanır.
    use crate::Work::*;

    // `Status::Poor`a eş değer.
    let status = Poor;
    // `Work::Civilian`a eş değer.
    let work = Civilian;

    match status {
        // Yukarıdaki aleni`use` nedeniyle kapsam açığına dikkat edin.
        Rich => println!("The rich have lots of money!"),
        Poor => println!("The poor have no money..."),
    }

    match work {
        // Kapsam açığını yeniden not edin.
        Civilian => println!("Civilians work!"),
        Soldier  => println!("Soldiers fight!"),
    }
}
```

### Ayrıca bakın:

[`match`][match] ve [`use`][use] 

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md
