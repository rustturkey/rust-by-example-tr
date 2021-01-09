# Hello World(Merhaba Dünya)

Geleneksel Hello World(Merhaba Dünya) programının kaynak kodu:

```rust,editable
// Bu bir yorum satırı, derleyici tarafından yok sayılır
// "Run" butonuna tıklayarak bu kodu test edebilirsiniz ->
// ya da klavyenizi kullanmayı tercih ederseniz, "Ctrl + Enter" kısayolunu kullanabilirsiniz

// Bu kod düzenlenebilir, kırmaktan çekinmeyin!
// Her zaman orijinal koda "Reset" butonuna tıklayarak dönebilirsiniz ->

// Bu ana fonksiyondur
fn main() {
    // Derlenen ikili(compiled binary) çağrıldığında ifadeler çalıştırılır 

    // Yazıyı konsola yazdır
    println!("Hello World!");
}
```

`println!` yazıları konsola yazdıran bir [*macro*][macros] 'dur.

Bir ikili(binary) `rustc` Rust derleyicisi kullanarak oluşturulabilir.

```bash
$ rustc hello.rs
```

`rustc` , çalıştırıldığında `hello` ikili(binary)si oluşturacaktır.

```bash
$ ./hello
Hello World!
```

### Aktivite

Beklenen çıktıyı görmek için 'Run' a tıklayın. Ardından, ikinci bir `println!` macro'su ekleyin ve çıktı şöyle görünecektir:

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md
