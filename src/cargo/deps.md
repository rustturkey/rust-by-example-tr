# Bağımlılıklar

Çoğu programın bazı kütüphanelere bağımlılıkları vardır. Hiç bağımlılıkları elle yönettiyseniz, bunun ne kadar acı verici olabileceğini tahmin edersiniz. Şanslıyız ki, Rust ekosistemi `cargo` ile standart olarak geliyor! `cargo` bir proje için bağımlılıkları yönetebilir.

Yeni bir Rust projesi oluşturmak için,

```sh
# A binary
cargo new foo

# OR A library
cargo new --lib foo
```

Bu bölümün geri kalanı için, bir kütüphane yerine bir ikili yaptığımızı varsayalım, ama tüm kavramlarımız aynı.

Yukarıdaki komutlardan sonra, aşağıdaki gibi bir dosya hiyerarşisi görmelisiniz:

```txt
foo
├── Cargo.toml
└── src
    └── main.rs
```

`main.rs` yeni projenizin root(kök/ana) kaynak dosyasıdır -- yeni bir şey yoktur.
`Cargo.toml` bu proje için `cargo` yapılandırma dosyasıdır (`foo`). İçine bakarsanız, şuna benzer bir şey görürsünüz:

```toml
[package]
name = "foo"
version = "0.1.0"
authors = ["mark"]

[dependencies]
```

`name` alanı `[package]` altındaki projenin adını belirler. Crate'i yayınlarsanız `crates.io` tarafından kullanılır(daha sonra anlatılacaktır). Ayrıca, derlediğinizde çıktı ikilisinin de adıdır.

`version` alanı [Semantic Versioning(Anlamsal Sürümlendirme)](http://semver.org/) kullanan crate sürüm numarasıdır.

`authors` alanı, crate'i yayınlarken kullanılan yazarların listesidir.

`[dependencies]` alanı projenize bağımlılık eklemenizi sağlar.

Örneğin, programınızın harika bir komut satırı arayüzüne sahip olmasını istediğinizi varsayalım. [crates.io](https://crates.io) (resmi Rust paket kayıtları)'da bir sürü güzel paket bulabilirsiniz. Popüler bir seçim [clap](https://crates.io/crates/clap)'tir.
Bu yazı boyunca, `clap`'in en son sürümü `2.27.1`'dir. Programımıza bir bağımlılık eklemek için,
`Cargo.toml` dosyamızda `[dependencies]`: `clap = "2.27.1"` şeklinde basitçe ekleriz. İşte budur! Artık programınızda
`clap` kullanmaya başlayabilirsiniz.

`cargo` [bağımlılıkların özel tipleri][dependencies]. Ufak bir özetleme:

```toml
[package]
name = "foo"
version = "0.1.0"
authors = ["mark"]

[dependencies]
clap = "2.27.1" # from crates.io
rand = { git = "https://github.com/rust-lang-nursery/rand" } # from online repo
bar = { path = "../bar" } # from a path in the local filesystem
```

`cargo` bir bağımlılık yöneticisinden daha fazlasıdır. Mevcut tüm konfigürasyon seçenekleri 
`Cargo.toml` 'deki [format belirleyici][manifest]de listelenmiştir.

Projemizi oluşturmak için, proje dizininde herhangi bir yerde (alt dizinler de dahil!) cargo'yu çalıştırırız. Aynı zamanda `cargo run` diyerek de build edip çalıştırabiliriz. Bu komutların tüm bağımlılıkları çözeceğine, gerekirse crate'leri indireceğine ve crate'iniz de dahil her şeyi oluşturacağını unutmayın! (Çoktan build edilmiş bir şeyi tekrar build ettiğini unutmayın `make`'e benzer şekilde).

İşte! Hepsi bu kadar!


[manifest]: https://doc.rust-lang.org/cargo/reference/manifest.html
[dependencies]: https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html
