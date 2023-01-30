# Nitelik

Nitelik yani `trait` bilinmeyen bir tip için tanımlanan metotlar koleksiyonudur:
`Self` (Kendi). Aynı nitelikte bildirilen diğer metotlara erişebilirler. 

Nitelikler herhangi bir veri tipi için uygulanabilirler. Aşağıdaki örnekte,
bir metot grubu olan `Animal`ı tanımlıyoruz. `Animal` `trait`(nitelik)i daha sonra 
`Sheep` veri tipi için uygulanarak `Animal` ve `Sheep`ten metotların kullanılmasına izin verir.

```rust,editable
struct Sheep { naked: bool, name: &'static str }

trait Animal {
    // Static metot imzası; `Self` implemente edici ifade eder.
    fn new(name: &'static str) -> Self;

    // Örnek metot imzaları; bunlar bir string döndürecektir.
    fn name(&self) -> &'static str;
    fn noise(&self) -> &'static str;

    // Nitelikler, varsayılan metot tanımlamaları sağlayabilir.
    fn talk(&self) {
        println!("{} says {}", self.name(), self.noise());
    }
}

impl Sheep {
    fn is_naked(&self) -> bool {
        self.naked
    }

    fn shear(&mut self) {
        if self.is_naked() {
            // İmplemente edici metotları, implemente edicinin nitelik metotlarını kullanabilir
            println!("{} is already naked...", self.name());
        } else {
            println!("{} gets a haircut!", self.name);

            self.naked = true;
        }
    }
}

// `Animal` niteliğini `Sheep` için implemente edin.
impl Animal for Sheep {
    // `Self`, implemente edici tipi: `Sheep`.
    fn new(name: &'static str) -> Sheep {
        Sheep { name: name, naked: false }
    }

    fn name(&self) -> &'static str {
        self.name
    }

    fn noise(&self) -> &'static str {
        if self.is_naked() {
            "baaaaah?"
        } else {
            "baaaaah!"
        }
    }
    
    // Varsayılan nitelik metotları geçersiz kılınabilir.
    fn talk(&self) {
        // Örneğin, biraz sessiz düşünme durağı ekleyebiliriz.
        println!("{} pauses briefly... {}", self.name, self.noise());
    }
}

fn main() {
    // Bu durumda, tip açıklaması gereklidir.
    let mut dolly: Sheep = Animal::new("Dolly");
    // YAPILACAK ^ Tip ek açıklamalarını kaldırmayı deneyin.

    dolly.talk();
    dolly.shear();
    dolly.talk();
}
```
