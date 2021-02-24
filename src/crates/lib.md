# Kütüphane Oluşturmak

Bir kütüphane oluşturalım, ve sonra onu başka bir crate'e bağlayacağımızı görelim.

```rust,ignore
pub fn public_function() {
    println!("called rary's `public_function()`");
}

fn private_function() {
    println!("called rary's `private_function()`");
}

pub fn indirect_access() {
    print!("called rary's `indirect_access()`, that\n> ");

    private_function();
}
```

```shell
$ rustc --crate-type=lib rary.rs
$ ls lib*
library.rlib
```

Kütüphaneler "lib" ön ekiyle başlarlar, ve varsayılan olarak crate dosyalarının adını alırlar, ama bu varsayılan ad,  `--crate-name` seçeneği ile `rustc`'ye iletilerek veya [`crate_name`
özelliği][crate-name] kullanılarak geçersiz kılınabilir.

[crate-name]: ../attribute/crate.md