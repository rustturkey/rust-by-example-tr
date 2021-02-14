# Hata Yönetimi

Hata yönetimi, başarısızlık olasılığını ele alma sürecidir. Örneğin, bir dosyayı okuyamamak ve *kötü* girdi kullanmaya devam etmek açık bir şekilde problemli olacaktır. Bu hataları fark etmek ve açıkça yönetmek, programın geri kalanını çeşitli tuzaklardan kurtarır.

Aşağıdaki alt bölümlerde açıklanan Rust'ta hatalarla başa çıkmanın çeşitli yolları vardır. Hepsinin az veya çok farklılıkları ve farklı kullanım durumları vardır. Kural olarak:

Açık bir `panic` temel olarak testler ve düzeltilemeyen hatalarla başa çıkmak için kullanışlıdır.
Prototipleme için, örneğin henüz implemente edilmemiş fonksiyonlarla uğraşırken kullanışlı olabilir, ama bu durumlarda daha açıklayıcı `implemente edilmemiş` daha iyidir. Testlerde `panic` açıkça başarısız olmanın mantıklı sebebidir.

`Option` tipi bir değerin isteğe bağlı olduğu veya bir değer eksikliğinin hata durumu olmadığı durumlar içindir.
Örneğin bir dizinin üstü - `/` ve `C:`den biri yok. `Option`lar ile uğraşırken, prototip oluşturma ve bir değer olacağının kesin olarak garantili olduğu kesinlikle kesin olan durumlarda `unwrap`(açma) uygundur. Bununla birlikte, `expect`(bekleme)
bir şeyler ters giderse diye bir hata mesajı belirlemenize izin verdiği için daha kullanışlıdır.

Bir şeylerin ters gitme ihtimali olduğunda ve çağırıcının sorunla ilgilenmesi gerektiğinde, `Result`(sonuç)ı kullanın. Aynı zamanda `unwrap`ve `expect` de yapabilirsiniz. (bir test veya hızlı prototip olmadıkça lütfen bunu yapmayın).

Hata işlemeye ilişkin daha titiz bir tartışma için [İngilizce Resmi Kitap][book]taki hata yönetimi bölümüne bakın.

[book]: https://doc.rust-lang.org/book/ch09-00-error-handling.html
