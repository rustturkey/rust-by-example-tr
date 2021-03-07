# Bir Kütüphaneyi Kullanmak

Bir crate'i yeni bir kütüphaneye bağlamak için `rustc`'nin `--extern` bayrağını kullanabilirsiniz. Tüm öğeler daha sonra kütüphaneyle aynı adda olan bir modülün altına aktarılacaktır
Bu modül genellikle diğer modüllerle aynı şekilde davranır.

```rust,ignore
// extern crate rary; // Rust 2015 sürümü veya öncesi için gerekli olabilir

fn main() {
    rary::public_function();

    // Hata alınır! `private_function` gizlidir
    //rary::private_function();

    rary::indirect_access();
}
```

```txt
# Where library.rlib is the path to the compiled library, assumed that it's
# in the same directory here:
$ rustc executable.rs --extern rary=library.rlib --edition=2018 && ./executable 
called rary's `public_function()`
called rary's `indirect_access()`, that
> called rary's `private_function()`
```
