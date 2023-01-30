# `From(-den)` ve `Into(biçimine)`

[`From`] ve [`Into`] doğaları gereği birbirine bağlı iki niteliktir, bu da aslında implementasyonlarının bir parçasıdır. Eğer A tipinden B tipine dönüşüm yapılabiliyorsa, B tipinden A tipine de kolaylıkla dönüşüm yapılabilir.

## `From`

[`From`] niteliği bir tipin kendisini başka tipten nasıl oluşturacağını tanımlamasına izin verir, bu nedenle birkaç tür arasında dönüştürme yapmak için çok basit bir mekanizma sağlar. Temel ve yaygın türlerin dönüştürülmesi için standart kütüphanede bu özelliğin çok sayıda implementasyonu vardır.

Örneğin `str` tipini kolayca `String` tipine dönüştürebiliriz.

```rust
let my_str = "hello";
let my_string = String::from(my_str);
```

Kendi tipimiz için bir dönüşüm tanımlamak için benzer bir şey yapabiliriz.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let num = Number::from(30);
    println!("My number is {:?}", num);
}
```

## `Into`

[`Into`] niteliği aslında basitçe `From` niteliğinin karşılığıdır.`From` niteliğini tanımladığınız tipinize implemente ettiyseniz `Into` gerekli olduğunda onu çağıracaktır.

`Into` niteliğini kullanmak genellikle, derleyici bunu çoğu zaman belirleyemediğinden dönüştürülecek tipin belirtilmesini gerektirir.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let int = 5;
    // Try removing the type annotation
    let num: Number = int.into();
    println!("My number is {:?}", num);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
