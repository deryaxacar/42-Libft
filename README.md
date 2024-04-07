<!-- Proje İlişkin Başlık -->
<h1 align="center">42 - Libft</h1>

<!-- Proje Açıklaması -->
<p align="center">
  `libft`, standart C kütüphanesindeki bazı temel işlevlerin nasıl çalıştığını anlamak için bir fırsat sunar. Genellikle, bu işlevleri yeniden uygulamak ve kendi kütüphanenizi oluşturmak istenen temel bir alıştırma olarak kullanılır. Bu işlevler, bellek işlemleri, dize manipülasyonu, karakter işlemleri ve listeler gibi çeşitli alanlara yayılmıştır.
</p>

<!-- Proje Logosu veya Görseli -->
<p align="center">
  <img src="https://github.com/ayogun/42-project-badges/blob/main/badges/libfte.png" alt="Proje Logo">
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
  - Prototip: `void *ft_memset(void *s, int c, size_t n);`
  - `s`: Belleği doldurulacak adresin başlangıç noktası.
  - `c`: Bellekte doldurulacak karakter.
  - `n`: Doldurulacak byte sayısı.
- **ft_bzero**: Belleği sıfırlar.
  - Prototip: `void ft_bzero(void *s, size_t n);`
  - `s`: Sıfırlanacak bellek bloğunun başlangıç adresi.
  - `n`: Sıfırlanacak byte sayısı.
- **ft_memcpy**: Bellek bloğunu kopyalar.
  - Prototip: `void *ft_memcpy(void *dest, const void *src, size_t n);`
  - `dest`: Kopyalanan verinin hedef adresi.
  - `src`: Kopyalanan verinin kaynak adresi.
  - `n`: Kopyalanacak byte sayısı.
- **ft_memmove**: Bellek bloğunu güvenli bir şekilde kopyalar.
  - Prototip: `void *ft_memmove(void *dest, const void *src, size_t n);`
  - `dest`: Kopyalanan verinin hedef adresi.
  - `src`: Kopyalanan verinin kaynak adresi.
  - `n`: Kopyalanacak byte sayısı.
- **ft_memchr**: Belirli bir karakteri bellekte arar.
  - Prototip: `void *ft_memchr(const void *s, int c, size_t n);`
  - `s`: Arama yapılacak bellek bloğunun adresi.
  - `c`: Aranan karakter.
  - `n`: Arama yapılacak maksimum byte sayısı.
- **ft_memcmp**: İki bellek bloğunu karşılaştırır.
  - Prototip: `int ft_memcmp(const void *s1, const void *s2, size_t n);`
  - `s1`: Karşılaştırılacak ilk bellek bloğunun adresi.
  - `s2`: Karşılaştırılacak ikinci bellek bloğunun adresi.
  - `n`: Karşılaştırılacak maksimum byte sayısı.

### Bellek İşlemleri Nedir?
<p align="left">
Bu işlevler, genellikle bellek alanının manipülasyonu ve işlenmesi gereken durumlarda kullanılır. Örneğin, bir dizi içinde belirli bir değerin aranması, bellek alanının belirli bir değerle doldurulması veya bellek bloklarının karşılaştırılması gibi işlemlerde bu fonksiyonlara ihtiyaç duyulur.
</p>

### Dize İşlemleri

- **ft_strlen**: Bir dizenin uzunluğunu hesaplar.
  - Prototip: `size_t ft_strlen(const char *s);`
  - `s`: Uzunluğu hesaplanacak dizi.
- **ft_strlcpy**: Bir dizenin bir başka diziye güvenli bir şekilde kopyalanması.
  - Prototip: `size_t ft_strlcpy(char *dst, const char *src, size_t size);`
  - `dst`: Kopyalanacak dizi.
  - `src`: Kaynak dizi.
  - `size`: Kopyalanacak maksimum byte sayısı.
- **ft_strlcat**: Bir dizenin bir başka dizeye güvenli bir şekilde eklenmesi.
  - Prototip: `size_t ft_strlcat(char *dst, const char *src, size_t size);`
  - `dst`: Dizeye eklenecek dizi.
  - `src`: Eklenen dizi.
  - `size`: Maksimum hedef dizinin boyutu.
- **ft_strchr**: Bir karakteri bir dizide arar.
  - Prototip: `char *ft_strchr(const char *s, int c);`
  - `s`: Arama yapılacak dizi.
  - `c`: Aranan karakter.
- **ft_strrchr**: Bir karakteri bir dizide sondan arar.
  - Prototip: `char *ft_strrchr(const char *s, int c);`
  - `s`: Arama yapılacak dizi.
  - `c`: Aranan karakter.
- **ft_strnstr**: Bir alt dizenin bir dizideki pozisyonunu bulur.
  - Prototip: `char *ft_strnstr(const char *haystack, const char *needle, size_t len);`
  - `haystack`: Arama yapılacak dizi.
  - `needle`: Aranan alt dizi.
  - `len`: Arama yapılacak maksimum karakter sayısı.
- **ft_strncmp**: İki dizeyi belirli bir sayıda karakterle karşılaştırır.
  - Prototip: `int ft_strncmp(const char *s1, const char *s2, size_t n);`
  - `s1`: Karşılaştırılacak ilk dizi.
  - `s2`: Karşılaştırılacak ikinci dizi.
  - `n`: Karşılaştırma yapılacak maksimum karakter sayısı.
- **ft_atoi**: Bir diziyi bir tam sayıya dönüştürür.
  - Prototip: `int ft_atoi(const char *str);`
  - `str`: Dönüştürülecek dizi.
- **ft_strdup**: Bir dizinin kopyasını yapar.
  - Prototip: `char *ft_strdup(const char *s);`
  - `s`: Kopyalanacak dizi.

### Dize İşlemleri Nedir?
<p align="left">
Dize işlemleri, metinsel verilerin manipülasyonu ve işlenmesi için kullanılan işlevlerdir. Bu işlevler, bir dizenin uzunluğunu hesaplamak, başka bir dizeye kopyalamak, bir dizeye yeni karakterler eklemek, belirli bir karakteri bir dizide aramak, alt dize aramak veya iki dizeyi karşılaştırmak gibi çeşitli işlemleri gerçekleştirir.
</p>

## Bonus Fonksiyonlar 
### Liste işlemleri

- **ft_lstnew**: Yeni bir liste düğümü oluşturur.
  - Prototip: `t_list *ft_lstnew(void *content);`
  - `content`: Düğümün içeriği.
- **ft_lstadd_front**: Başa bir düğüm ekler.
  - Prototip: `void ft_lstadd_front(t_list **lst, t_list *new);`
  - `lst`: Düğümün ekleneceği liste.
  - `new`: Eklenecek düğüm.
- **ft_lstsize**: Listenin eleman sayısını döndürür.
  - Prototip: `int ft_lstsize(t_list *lst);`
  - `lst`: Boyutu hesaplanacak liste.
- **ft_lstlast**: Listenin son elemanını döndürür.
  - Prototip: `t_list *ft_lstlast(t_list *lst);`
  - `lst`: Son elemanın bulunacağı liste.
- **ft_lstadd_back**: Sona bir düğüm ekler.
  - Prototip: `void ft_lstadd_back(t_list **lst, t_list *new);`
  - `lst`: Düğümün ekleneceği liste.
  - `new`: Eklenecek düğüm.
- **ft_lstdelone**: Belirli bir düğümü siler.
  - Prototip: `void ft_lstdelone(t_list *lst, void (*del)(void*));`
  - `lst`: Silinecek düğüm.
  - `del`: Düğüm içeriğini silen işlev.
- **ft_lstclear**: Tüm listeyi siler.
  - Prototip: `void ft_lstclear(t_list **lst, void (*del)(void*));`
  - `lst`: Silinecek liste.
  - `del`: Düğüm içeriğini silen işlev.
- **ft_lstiter**: Bir fonksiyonu her liste elemanı için çağırır.
  - Prototip: `void ft_lstiter(t_list *lst, void (*f)(void*));`
  - `lst`: İşlem yapılacak liste.
  - `f`: Her düğüm için çağrılacak işlev.
- **ft_lstmap**: Bir fonksiyonu her liste elemanı için çağırır ve yeni bir liste oluşturur.
  - Prototip: `t_list *ft_lstmap(t_list *lst, void *(*f)(void*), void (*del)(void*));`
  - `lst`: Kaynak liste.
  - `f`: Her düğüm için çağrılacak işlev.
  - `del`: Düğüm içeriğini silen işlev.

### Liste İşlemleri Nedir?
<p align="left">
Liste işlemleri, verilerin düğüm adı verilen birimler halinde organize edilmesi ve işlenmesi için kullanılan işlevlerdir. Bu işlevler, bir veri yapısında yeni bir düğüm oluşturmak, düğüm eklemek, düğüm silmek, düğüm aramak, düğüm sayısını hesaplamak gibi çeşitli işlemleri gerçekleştirir.
</p>
