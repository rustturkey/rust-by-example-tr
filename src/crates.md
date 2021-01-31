# Crate'ler(Sandıklar)

Crate Rust'ta bir derleme birimidir. `rustc herhangi_bir_dosya.rs` çağrıldığında,
`herhangi_bir_dosya.rs`  *crate dosyası*  olarak kabul edilir. Eğer `herhangi_bir_dosya.rs` 'da `mod`
bildirimi varsa, daha sonra modül dosyalarının içeriği derleyici üzerinde çalışmadan *önce* crate dosyasındaki `mod` bildirimlerinin bulunduğu yere eklenir. Diğer bir deyişle, modüller ayrı ayrı derlen*mez* sadece crate'ler(sandıklar) derlenir.

Bir crate bir ikili dosyaya veya kütüphaneye derlenebilir. Varsayılan olarak, `rustc`
bir crate'den bir ikili dosya üretecektir. Bu davranış `--crate-type` bayrağını `lib` 'e ileterek geçersiz kılınabilir.
