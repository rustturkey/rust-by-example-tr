# Betik(Script) Oluşturmak

Bazen `cargo` ile normal oluşturmalar yeterli olmaz. Belki `cargo` başarılı bir şekilde derlenmeden önce crate'inizin bazı ön koşullara, veya derlenmesi gereken bazı yerel kodlara ihtiyacı vardır. Bu problemi çözmek için Cargo'nun çalıştırabileceği bazı betikler yazarız.

Paketinize betik eklemek için, `Cargo.toml` dosyasında aşağıdaki gibi belirtilebilir:

```toml
[package]
...
build = "build.rs"
```

Aksi halde Cargo varsayılan olarak proje dizinindeki `build.rs` dosyasını kullanacaktır.

## Yazılmış betiği nasıl kullanırız

Betik paketteki herhangi bir şeyi derlemeden önce derlenecek ve çağrılacak başka bir Rust dosyasıdır. Dolayısıyla crate'inizin ön koşullarını yerine getirmek için kullanılabilir.

Cargo betiğe, [burada belirtilen][specified here] ve kullanılabilecek ortam değişkenleri aracılığıyla input(girdi)'lar sağlar.

Betik, stdout aracılığıyla output(çıktı) sağlar. Tüm satırlar
`target/debug/build/<pkg>/output` konumuna yazılır. Dahası, `cargo:`yla ön eklenmiş satırlar: doğrudan cargo tarafından yorumlanacaktır ve bu nedenle paketin derlenmesi için parametreleri tanımlamak için kullanılabilir.

Daha ileri seviyede tanım ve örnekler için 
[İngilizce Cargo kitabından bir bölüm][cargo_specification].

[specified here]: https://doc.rust-lang.org/cargo/reference/environment-variables.html#environment-variables-cargo-sets-for-build-scripts

[cargo_specification]: https://doc.rust-lang.org/cargo/reference/build-scripts.html
