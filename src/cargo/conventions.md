# Kurallar

Önceki bölümde, aşağıdaki dizin hiyerarşisini görmüştük:

```txt
foo
├── Cargo.toml
└── src
    └── main.rs
```

Yine de aynı projede iki ikiliye ihtiyacımız olduğunu varsayalım. Ne olacak?

`cargo`nun bunu desteklediğini görürüz. Varsayılan ikili dosya ismi daha önce de gördüğünüz gibi `main`'dir, ama bunları bir `bin/` dizinine yerleştirerek ek ikili dosyalar ekleyebilirsiniz:

```txt
foo
├── Cargo.toml
└── src
    ├── main.rs
    └── bin
        └── my_other_bin.rs
```

`cargo`ya varsayılan veya diğer ikili dosyaların aksine bu ikiliyi derlemesini veya çalıştırmasını söylemek için sadece `cargo`dan `--bin my_other_bin` bayrağını geçiyoruz(pass ediyoruz), burada `my_other_bin` çalışmak istediğimiz ikili dosyanın adıdır.

Extra binaries(ekstra ikili)'lere ek olarak `cargo` kıyaslama(benchmark) testler ve örnekler gibi [daha fazla] özelliği destekler.

Gelecek bölümde, test(deneme)lere daha yakından bakacağız.

[daha fazla]: https://doc.rust-lang.org/cargo/guide/project-layout.html
