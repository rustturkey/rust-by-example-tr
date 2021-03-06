# Özet

[Giriş](index.md)

- [Hello World(Merhaba Dünya)](hello.md)
    - [Yorumlar](hello/comment.md)
    - [Formatlı Yazdırma](hello/print.md)
        - [Hata Ayıkla](hello/print/print_debug.md)
        - [Görüntüle](hello/print/print_display.md)
            - [Deneme: Liste](hello/print/print_display/testcase_list.md)
        - [Formatlama](hello/print/fmt.md)

- [Temeller](primitives.md)
    - [Literaller ve Operatörler](primitives/literals.md)
    - [Tuple'lar(Veri Tabanındaki Veri Grupları)](primitives/tuples.md)
    - [Diziler ve Dilimleri](primitives/array.md)

- [Özel Tipler](custom_types.md)
    - [Structure'lar(Yapılar)](custom_types/structs.md)
    - [Enum'lar](custom_types/enum.md)
        - [kullanım](custom_types/enum/enum_use.md)
        - [C-gibi](custom_types/enum/c_like.md)
        - [Deneme: bağlı liste](custom_types/enum/testcase_linked_list.md)
    - [sabitler](custom_types/constants.md)

- [Değişken Bağlama](variable_bindings.md)
    - [Değişebilirlik](variable_bindings/mut.md)
    - [Kapsam ve Öncelik](variable_bindings/scope.md)
    - [Önce Bildir](variable_bindings/declare.md)
    - [Donma](variable_bindings/freeze.md)

- [Tipler](types.md)
    - [Kalıplama](types/cast.md)
    - [Literal'ler](types/literals.md)
    - [Belirleme](types/inference.md)
    - [Referanslama](types/alias.md)

- [Dönüşümler](conversion.md)
    - [`From` and `Into`](conversion/from_into.md)
    - [`TryFrom` and `TryInto`](conversion/try_from_try_into.md)
    - [To and from `String`s](conversion/string.md)

- [İfadeler](expression.md)
   
- [Kontrol Akışı](flow_control.md)
    - [if/else](flow_control/if_else.md)
    - [döngü](flow_control/loop.md)
        - [İç içe ve etiketli](flow_control/loop/nested.md)
        - [Döngülerden return(geridönüş alma)](flow_control/loop/return.md)
    - [while](flow_control/while.md)
    - [for ve aralık](flow_control/for.md)
    - [eşleşme](flow_control/match.md)
        - [Yıkmak](flow_control/match/destructuring.md)
            - [tuple'lar (veri tabanındaki veri grupları)](flow_control/match/destructuring/destructure_tuple.md)
            - [enum'lar](flow_control/match/destructuring/destructure_enum.md)
            - [işsaretçiler/referanslar](flow_control/match/destructuring/destructure_pointers.md)
            - [struct'lar(yapılar)](flow_control/match/destructuring/destructure_structures.md)
        - [Denetleyiciler](flow_control/match/guard.md)
        - [Bağlama](flow_control/match/binding.md)
    - [if let](flow_control/if_let.md)
    - [while let](flow_control/while_let.md)

- [Fonksiyonlar](fn.md)
    - [Metotlar](fn/methods.md)
    - [Closure'lar(Kapatıcılar)](fn/closures.md)
        - [Yakalama](fn/closures/capture.md)
        - [Girdi Olarak Parametreler](fn/closures/input_parameters.md)
        - [Tip Anonimliği](fn/closures/anonymity.md)
        - [Girdi Fonksiyonları](fn/closures/input_functions.md)
        - [Çıktı Olarak Parametreler](fn/closures/output_parameters.md)
        - [`std` ile Örnekler](fn/closures/closure_examples.md)
            - [Iterator::any](fn/closures/closure_examples/iter_any.md)
            - [Yineleyicilerde Arama](fn/closures/closure_examples/iter_find.md)
    - [Üst Seviye Fonksiyonlar](fn/hof.md)
    - [Ayrık Fonksiyonlar](fn/diverging.md)

- [Modüller](mod.md)
    - [Görünürlük](mod/visibility.md)
    - [Struct(yapı) görünürlüğü](mod/struct_visibility.md)
    - [`use` bildirimi](mod/use.md)
    - [`super` ve `self`](mod/super.md)
    - [Dosya Hiyerarşisi](mod/split.md)

- [Crates(Sandıklamak)](crates.md)
    - [Kütüphane Oluşturmak](crates/lib.md)
    - [Kütüphane Kullanmak](crates/using_lib.md)

- [Cargo](cargo.md)
    - [Bağlılıklar](cargo/deps.md)
    - [Dönüşümler](cargo/conventions.md)
    - [Denemeler](cargo/test.md)
    - [Komut İnşası](cargo/build_scripts.md)

- [Özellikler](attribute.md)
    - [`dead_code`](attribute/unused.md)
    - [Crates](attribute/crate.md)
    - [`cfg`](attribute/cfg.md)
         - [Özelleştirilmiş](attribute/cfg/custom.md)

- [Generic'ler(Genelleyiciler)](generics.md)
    - [Fonksiyonlar](generics/gen_fn.md)
    - [İmplementasyon](generics/impl.md)
    - [Nitelikler](generics/gen_trait.md)
    - [Sınırlar](generics/bounds.md)
        - [Deneme: boş sınırlar](generics/bounds/testcase_empty.md)
    - [Çoklu Sınırlar](generics/multi_bounds.md)
    - [Where Koşulları](generics/where.md)
    - [New Type Deyimi](generics/new_types.md)
    - [Bağlantılı Maddeler](generics/assoc_items.md)
        - [Problem](generics/assoc_items/the_problem.md)
        - [Bağlantılı Tipler](generics/assoc_items/types.md)
    - [Siluet Tipli Parametreler](generics/phantom.md)
        - [Deneme: Birim belirtme](generics/phantom/testcase_units.md)

- [Kapsam Kuralları](scope.md)
    - [RAII](scope/raii.md)
    - [Mülkiyet ve Hamleler](scope/move.md)
        - [Değişebilirlik](scope/move/mut.md)
        - [Kısmi Hamleler](scope/move/partial_move.md)
    - [Alıntılar](scope/borrow.md)
        - [Değişebilirlik](scope/borrow/mut.md)
        - [Örtüşme](scope/borrow/alias.md)
        - [Ref Deseni](scope/borrow/ref.md)
    - [Yaşam Boyu](scope/lifetime.md)
        - [Net Açıklama](scope/lifetime/explicit.md)
        - [Fonksiyonlar](scope/lifetime/fn.md)
        - [Metotlar](scope/lifetime/methods.md)
        - [Struct'lar(Yapılar)](scope/lifetime/struct.md)
        - [Nitelikler](scope/lifetime/trait.md)
        - [Sınırlar](scope/lifetime/lifetime_bounds.md)
        - [Baskı](scope/lifetime/lifetime_coercion.md)
        - [Sabit](scope/lifetime/static_lifetime.md)
        - [Çıkarma/Düşme](scope/lifetime/elision.md)

- [Nitelikler](trait.md)
    - [Türemek](trait/derive.md)
    - [Niteliklerde`dyn` ile geridönüş(return) alma](trait/dyn.md)
    - [Operatöre Aşırı Yükleme(Overloading)](trait/ops.md)
    - [Alçalma](trait/drop.md)
    - [Yineleyiciler](trait/iter.md)
    - [`impl Trait`](trait/impl_trait.md)
    - [Klon](trait/clone.md)
    - [Süpernitelikler](trait/supertraits.md)
    - [Niteliklerde örtüşümle belirginleştirme](trait/disambiguating.md)

- [macro_rules!(Makro Kuralları)](macros.md)
    - [Sözdizimi](macros/syntax.md)
        - [Düzenleyiciler](macros/designators.md)
        - [Aşırı Yükleme](macros/overload.md)
        - [Tekrar](macros/repeat.md)
    - [DRY (Don't Repeat Yourself)(Kendini Tekrarlama)](macros/dry.md)
    - [DSL (Domain Specific Languages)(Belirli Alan Dilleri)](macros/dsl.md)
    - [Variadic'ler(Değişken Sayıda Argüman Alabilen Fonksiyonlar)](macros/variadics.md)

- [Hata Yönetimi](error.md)
    - [`panic`](error/panic.md)
    - [`Option` & `unwrap`](error/option_unwrap.md)
        - [Özellikleri `?` ile paketinden çıkarma](error/option_unwrap/question_mark.md)
        - [Birleştiriciler: `map`](error/option_unwrap/map.md)
        - [Birleştiriciler: `and_then`](error/option_unwrap/and_then.md)
    - [`Result`](error/result.md)
        - [`map` için `Result`](error/result/result_map.md)
        - [Örtüşmeler için `Result`](error/result/result_alias.md)
        - [Erken return'ler(geri dönüşler)](error/result/early_returns.md)
        - [`?` 'ne giriş](error/result/enter_question_mark.md)
    - [Çoklu Hata Tipleri](error/multiple_error_types.md)
        - [`Option`(Özellik)lerden `Result`(Sonuç)ları çekme](error/multiple_error_types/option_result.md)
        - [Hata tipi tanımlama](error/multiple_error_types/define_error_type.md)
        - [Hataları `Box`(Kutu)lama](error/multiple_error_types/boxing_errors.md)
        - [`?`nin diğer kullanımları](error/multiple_error_types/reenter_question_mark.md)
        - [Hataları sarma](error/multiple_error_types/wrap_error.md)
    - [`Result`(Sonuç)ları yineletme](error/iter_result.md)

- [Std kütüphanesi tipleri](std.md)
    - [Box, stack and heap(Kutu, yığın ve öbek)](std/box.md)
    - [Vectörler](std/vec.md)
    - [String'ler(Dizeler)](std/str.md)
    - [`Option`](std/option.md)
    - [`Result`](std/result.md)
        - [`?`](std/result/question_mark.md)
    - [`panic!`](std/panic.md)
    - [HashMap'ler](std/hash.md)
        - [Alternate/custom key types](std/hash/alt_key_types.md)
        - [HashSet](std/hash/hashset.md)
    - [`Rc`](std/rc.md)
    - [`Arc`](std/arc.md)

- [Std diğer](std_misc.md)
    - [Thread'ler](std_misc/threads.md)
        - [Testcase: map-reduce](std_misc/threads/testcase_mapreduce.md)
        - [Kanallar](std_misc/channels.md)
    - [Yollar](std_misc/path.md)
    - [Dosya G/Ç](std_misc/file.md)
        - [`open`(aç)](std_misc/file/open.md)
        - [`create`(yarat)](std_misc/file/create.md)
        - [`read lines`(satır oku)](std_misc/file/read_lines.md)
    - [Child processes(Alt İşlemler)](std_misc/process.md)
        - [Pipes(Borular)](std_misc/process/pipe.md)
        - [Wait(Bekleme)](std_misc/process/wait.md)
    - [Dosya Sistemi İşlemleri](std_misc/fs.md)
    - [Program Argümanları](std_misc/arg.md)
        - [Argüman Ayırma](std_misc/arg/matching.md)
    - [Yabancı Fonksiyon Arayüzü](std_misc/ffi.md)

- [Deneme](testing.md)
    - [Birim Testleri](testing/unit_testing.md)
    - [Dokümantasyon Tesleri](testing/doc_testing.md)
    - [Entegrasyon Testleri](testing/integration_testing.md)
    - [Geliştiriciye bağlı olan testler](testing/dev_dependencies.md)

- [Güvensiz İşlemler](unsafe.md)

- [Uyumluluk](compatibility.md)
    - [Ham Belirteçler](compatibility/raw_identifiers.md)

- [Üst](meta.md)
    - [Dokümantasyon](meta/doc.md)
    - [Evcik](meta/playpen.md)
