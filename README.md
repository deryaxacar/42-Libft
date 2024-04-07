<!-- Proje İlişkin Başlık -->
<h1 align="center">42 - Libft</h1>

<!-- Proje Açıklaması -->
<p align="center">
  `libft`, standart C kütüphanesindeki bazı temel işlevlerin nasıl çalıştığını anlamak için bir fırsat sunar. Genellikle, bu işlevleri yeniden uygulamak ve kendi kütüphanenizi oluşturmak istenen temel bir alıştırma olarak kullanılır. Bu işlevler, bellek işlemleri, dize manipülasyonu, karakter işlemleri ve listeler gibi çeşitli alanlara yayılmıştır.
</p>

<!-- Proje Logosu veya Görseli -->
<p align="center">
  <img src="https://github.com/byaliego/42-project-badges/blob/main/badges/libftm.png" alt="Proje Logo">
</p>

<!-- Proje Başlıkları ve İçindekiler -->
## İçindekiler
- [Gereksinimler](#gereksinimler)
- [Kullanım](#kullanım)
- [Fonksiyonlar](#fonksiyonlar)

<!-- Gereksinimler -->
## Gereksinimler

Projeyi çalıştırmak için herhangi bir özel gereksinim yoktur. Sadece C derleyicisine (gcc gibi) ve bir terminal arayüzüne ihtiyacınız vardır.

<!-- Kullanım -->
## Kullanım

Projeyi kullanmak için aşağıdaki adımları izleyebilirsiniz:

1. Libft kütüphanesini indirin veya kendi projenize ekleyin.
2. `#include "libft.h"` ifadesini projenizin başlangıcına ekleyin.
3. İlgili fonksiyonları kullanarak projenizi geliştirin.

<!-- Fonksiyonlar -->
## Fonksiyonlar

### Bellek İşlemleri

- **ft_memset**: Belleği belirli bir değerle doldurur.
- **ft_bzero**: Belleği sıfırlar.
- **ft_memcpy**: Bellek bloğunu kopyalar.
- **ft_memccpy**: Karakter bulunana kadar bellek bloğunu kopyalar.
- **ft_memmove**: Bellek bloğunu güvenli bir şekilde kopyalar.
- **ft_memchr**: Belirli bir karakteri bellekte arar.
- **ft_memcmp**: İki bellek bloğunu karşılaştırır.

### Dize İşlemleri

- **ft_strlen**: Bir dizenin uzunluğunu hesaplar.
- **ft_strlcpy**: Bir dizenin bir başka diziye güvenli bir şekilde kopyalanması.
- **ft_strlcat**: Bir dizenin bir başka dizeye güvenli bir şekilde eklenmesi.
- **ft_strchr**: Bir karakteri bir dizide arar.
- **ft_strrchr**: Bir karakteri bir dizide sondan arar.
- **ft_strnstr**: Bir alt dizenin bir dizideki pozisyonunu bulur.
- **ft_strncmp**: İki dizeyi belirli bir sayıda karakterle karşılaştırır.
- **ft_atoi**: Bir diziyi bir tam sayıya dönüştürür.
- **ft_strdup**: Bir dizinin kopyasını yapar.

### Bonus Fonksiyonlar

- **ft_lstnew**: Yeni bir liste düğümü oluşturur.
- **ft_lstadd_front**: Başa bir düğüm ekler.
- **ft_lstsize**: Listenin eleman sayısını döndürür.
- **ft_lstlast**: Listenin son elemanını döndürür.
- **ft_lstadd_back**: Sona bir düğüm ekler.
- **ft_lstdelone**: Belirli bir düğümü siler.
- **ft_lstclear**: Tüm listeyi siler.
- **ft_lstiter**: Bir fonksiyonu her liste elemanı için çağırır.
- **ft_lstmap**: Bir fonksiyonu her liste elemanı için çağırır ve yeni bir liste oluşturur.
