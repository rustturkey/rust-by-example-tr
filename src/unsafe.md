# Güvensiz İşlemler

Bu bölüme girerken, [resmi İngilizce doküman][unsafe]lardan bir alıntı olarak,
"Bir kod tabanındaki güvenli olmayan kod miktarı en aza indirilmeye çalışılmalıdır." Aklımıza bunu kazıyarak, hadi başlayalım! Rust'taki güvenli olmayan ek açıklamalar, derleyici tarafından uygulanan korumaları atlatmak için kullanılır; özellikle güvenli olmayan dört temel şey:

* açık(veya ham diye ifade edilir) pointer'ı derefere etme(refere ettiği yerden ayırma)
* `unsafe`(güvensiz) olan fonksiyon veya metotları çağırma (FFI üzerinden bir fonksiyonu çağırmak da buna dahil, [kitabın bir önceki bölümü](std_misc/ffi.md)ne bakın.) 
* static mutable(değişebilir) değişkenlere erişmek veya bunları değiştirmek
* unsafe(güvensiz) trait'ler implemente etmek

### Açık pointer'lar
Açık pointer'lar `*` ve referanslar `&T` benzer şekilde çalışırlar, ama referanslar her zaman güvenlidir çünkü ödünç alma(borrow) denetleyicisi ile geçerli verilere işaret etmeleri garanti edilir. Açık bir göstericinin referansının kaldırılması sadece güvenli olmayan bir blok aracılığıyla yapılabilir.

```rust,editable
fn main() {
    let raw_p: *const u32 = &10;

    unsafe {
        assert!(*raw_p == 10);
    }
}
```

### Unsafe(Güvensiz) Fonksiyonların Çağrımı
Bazı fonksiyonlar `unsafe`(güvensiz) olarak bildirilebilir, bu derleyicinin yerine doğruluğu sağlamak programcının sorumluluğundadır. Buna bir örnek: [`std::slice::from_raw_parts`] ilk elemana bir pointer ve bir uzunluk verilen bir hafıza dilimi ayıracaktır.

```rust,editable
use std::slice;

fn main() {
    let some_vector = vec![1, 2, 3, 4];

    let pointer = some_vector.as_ptr();
    let length = some_vector.len();

    unsafe {
        let my_slice: &[u32] = slice::from_raw_parts(pointer, length);

        assert_eq!(some_vector.as_slice(), my_slice);
    }
}
```

`slice::from_raw_parts` için, onaylanması gereken varsayımlardan biri, pointer'ın geçerli belleğe geçirilmesi ve işaret edilen belleğin doğru tipte olmasıdır. Bu değişmezler korunmazsa, programın davranışı tanımsızdır ve ne olacağını bilemeyiz.


[unsafe]: https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html
[`std::slice::from_raw_parts`]: https://doc.rust-lang.org/std/slice/fn.from_raw_parts.html
