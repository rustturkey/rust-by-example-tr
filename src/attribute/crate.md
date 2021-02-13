# Crate'ler (Sandıklar)

`crate_type` özelliği, derleyiciye crate'in bir binary(ikili) dosya mı yoksa kütüphane dosyası mı olduğunu bildirmek  için kullanılabilir, (ve hatta hangi tipte bir kütüphane olduğunu), ve `crate_name` özelliği, crate'in adını ayarlamak için kullanılabilir.

Bununla birlikte, Rust paket yöneticisi Cargo kullanırken hem `crate_type` hem de `crate_name`
özelliklerinin **hiçbir** etkisi olmadığını unutmamak önemlidir. Cargo, Rust projelerinin büyük çoğunluğunda kullanıldığından,  `crate_type` ve `crate_name`'in gerçek dünyadaki kullanımlarının göreli olarak sınırlı olduğu anlamına gelir.

```rust,editable
// Bu crate bir kütüphanedir(library)
#![crate_type = "lib"]
// Bu kütüphanenin adı "rary"dir
#![crate_name = "rary"]

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

`crate_type` özelliği kullanıldığında, artık `--crate-type` bayrağını `rustc` iletmek gerekmez.

```shell
$ rustc lib.rs
$ ls lib*
library.rlib
```
