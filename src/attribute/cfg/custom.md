# Özel 

`target_os` gibi bazı koşul ifadeleri dolaylı olarak `rustc` tarafından sağlanır, ama özel koşul ifadeleri `--cfg` bayrağı kullanılarak `rustc`ye iletilmelidir.

```rust,editable,ignore,mdbook-runnable
#[cfg(birtakim_kosullar)]
fn kosullu_fonksiyon() {
    println!("kosul karsilandi!");
}

fn main() {
    kosullu_fonksiyon();
}
```

Bunu özel `cfg` bayrağı olmadan çalıştırın ve bakın neler oluyor.

Özel `cfg` bayrağıyla:

```shell
$ rustc --cfg birtakim_kosullar custom.rs && ./custom
kosul karsilandi!
```
