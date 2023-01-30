# macro_rules!

Rust, metaprogramlamaya izin veren güçlü bir macro sistemi sağlar. Önceki bölümlerde gördüğünüz gibi, macro'lar fonksiyonlara benziyor, ancak adlarının bir `!` patlamasıyla bitmesi dışında, ancak bir fonksiyon çağrısı oluşturmak yerine, macro'lar programın geri kalanıyla derlenen kaynak koduna genişletilir.
Bununla birlikte, C ve diğer dillerdeki macro'lardan farklı olarak, Rust macro'ları string ön işlemesi yerine soyut(abstract) söz dizimi ağaçlarına genişletilir, böylece beklenmedik öncelik hataları alınmaz.

Macro'lar `macro_rules!` macro'su kullanılarak oluşturulur.

```rust,editable
// `say_hello` isimli basit bir macro.
macro_rules! say_hello {
    // `()` macro'nun argüman almadığını belirtir.
    () => {
        // Macro bu bloğun içeriklerini genişletir.
        println!("Hello!");
    };
}

fn main() {
    // Bu çağrım `println!("Hello");` e genişletir
    say_hello!()
}
```

Macro'lar neden kullanışlıdır?

1. Kendini tekrar etmez. Birden çok yerde, ancak farklı türlerde benzer fonksiyoneliteye ihtiyaç duyabileceğiniz birçok durum vardır. Genellikle bir macro yazmak, kodun tekrarlanmasını önlemenin yararlı bir yoludur. (Bununla ilgili daha fazlası sonra...)

2. Etki alanına özgü diller. Macro'lar belirli bir amaç için özel söz dizimi tanımlanmasına izin verir.(Bununla ilgili daha fazlası sonra...)

3. Çeşitli interface(arayüz)'ler. Bazen değişken sayısında argüman alan bir interface tanımlamak istersiniz. Bir örnek olarak `println!`  string'in biçimine bağlı olarak herhangi bir sayıda argüman alabilir.(Bununla ilgili daha fazlası sonra...)
