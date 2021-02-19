# Test

Bildiğiniz gibi, test herhangi bir yazılımın ayrılmaz bir parçasıdır! Rust birim ve entegrasyon testi için birinci sınıf desteğe sahiptir ([resmi dokümandaki bu bölüme](https://doc.rust-lang.org/book/ch11-00-testing.html) bakın.

Yukarıda bağlantılı test bölümlerinden, birim testleri ve entegrasyon testlerinin nasıl yazılacağını görüyoruz. Organizasyonel olarak birim testlerini test ettikleri modüllere ve entegrasyon testlerini kendini `tests/` dizinine yerleştirebiliriz:

```txt
foo
├── Cargo.toml
├── src
│   └── main.rs
└── tests
    ├── my_test.rs
    └── my_other_test.rs
```

`tests` dizinindeki tüm dosyalar ayrı bir entegrasyon testidir.

`cargo` yapısından gelen özelliğiyle tüm testlerinizi çalıştırmak için kolay yol sunar!

```shell
$ cargo test
```

Şöyle bir çıktı alırsınız:

```shell
$ cargo test
   Compiling blah v0.1.0 (file:///nobackup/blah)
    Finished dev [unoptimized + debuginfo] target(s) in 0.89 secs
     Running target/debug/deps/blah-d3b32b97275ec472

running 3 tests
test test_bar ... ok
test test_baz ... ok
test test_foo_bar ... ok
test test_foo ... ok

test result: ok. 3 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
```

Ayrıca adı bir desenle(pattern ile) eşleşen testleri de çalıştırabilirsiniz:

```shell
$ cargo test test_foo
```

```shell
$ cargo test test_foo
   Compiling blah v0.1.0 (file:///nobackup/blah)
    Finished dev [unoptimized + debuginfo] target(s) in 0.35 secs
     Running target/debug/deps/blah-d3b32b97275ec472

running 2 tests
test test_foo ... ok
test test_foo_bar ... ok

test result: ok. 2 passed; 0 failed; 0 ignored; 0 measured; 2 filtered out
```

Bir uyarı: Cargo aynı anda birden fazla test yapabilir, bu yüzden birbirleriyle yarışmadıklarından emin olun. Örneğin, hepsi bir dosyaya çıktı veriyorsa, onları farklı dosyalara yazdırmalısınız.
