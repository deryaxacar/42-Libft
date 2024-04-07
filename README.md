<!-- Proje İlişkin Başlık -->
<h1 align="center">42 - Libft</h1>

<!-- Proje Açıklaması -->
<p align="center">
  `libft`, standart C kütüphanesindeki bazı temel işlevlerin nasıl çalıştığını anlamak için bir fırsat sunar. Genellikle, bu işlevleri yeniden uygulamak ve kendi kütüphanenizi oluşturmak istenen temel bir alıştırma olarak kullanılır. Bu işlevler, bellek işlemleri, dize manipülasyonu, karakter işlemleri ve listeler gibi çeşitli alanlara yayılmıştır.
</p>

<!-- Proje Logosu veya Görseli -->
<p align="center">
  <img src="https://github.com/ayogun/42-project-badges/blob/main/badges/libftm.png" alt="Proje Logo">
</p>

<!-- Proje Başlıkları ve İçindekiler -->
## İçindekiler

- [Gereksinimler](#gereksinimler)
- [Kullanım](#kullanım)
- [Fonksiyonlar](#fonksiyonlar)
- [Kullanım](#kullanım)
- [Bonus Fonksiyonlar](#bonus-fonksiyonlar)
- [Notlar](#notlar)
  
<!-- Gereksinimler -->
## Gereksinimler

Projeyi çalıştırmak için herhangi bir özel gereksinim yoktur. Sadece C derleyicisine (gcc gibi) ve bir terminal arayüzüne ihtiyacınız vardır.

<!-- Kullanım -->
## Kullanım

Projeyi kullanmak için aşağıdaki adımları izleyebilirsiniz:

1. Sağ Üstteki `<> Code` kısmına tıklayın.
2. Daha sonra `Download Zip` kısmına tıklayın ve zip dosyasını indirin.
3. Bilgisayarınızdaki zip dosyasını açın.

<!-- Fonksiyonlar -->
## Fonksiyonlar

### Bellek İşlemleri

- **ft_memset**: Belleği belirli bir değerle doldurur.
  - Prototip: `void *ft_memset(void *s, int c, size_t n);`
  - `s`: Belleği doldurulacak adresin başlangıç noktası.
  - `c`: Bellekte doldurulacak karakter.
  - `n`: Doldurulacak byte sayısı.
  - Dönüş Değeri: Başlangıç adresini içeren bir işaretçi (s).

- **ft_bzero**: Belleği sıfırlar.
  - Prototip: `void ft_bzero(void *s, size_t n);`
  - `s`: Sıfırlanacak bellek bloğunun başlangıç adresi.
  - `n`: Sıfırlanacak byte sayısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_calloc**: Belirtilen boyutta bellek bloğu tahsis eder ve sıfırlar.
  - Prototip: `void *ft_calloc(size_t count, size_t size);`
  - `count`: Tahsis edilecek öğe sayısı.
  - `size`: Her öğenin boyutu (byte cinsinden).
  - Dönüş Değeri: Tahsis edilen bellek bloğunun başlangıç adresini içeren bir işaretçi.

- **ft_memcpy**: Bellek bloğunu kopyalar.
  - Prototip: `void *ft_memcpy(void *dest, const void *src, size_t n);`
  - `dest`: Kopyalanan verinin hedef adresi.
  - `src`: Kopyalanan verinin kaynak adresi.
  - `n`: Kopyalanacak byte sayısı.
  - Dönüş Değeri: Hedef adresi içeren bir işaretçi (dest).

- **ft_memmove**: Bellek bloğunu güvenli bir şekilde kopyalar.
  - Prototip: `void *ft_memmove(void *dest, const void *src, size_t n);`
  - `dest`: Kopyalanan verinin hedef adresi.
  - `src`: Kopyalanan verinin kaynak adresi.
  - `n`: Kopyalanacak byte sayısı.
  - Dönüş Değeri: Hedef adresi içeren bir işaretçi (dest).

- **ft_memchr**: Belirli bir karakteri bellekte arar.
  - Prototip: `void *ft_memchr(const void *s, int c, size_t n);`
  - `s`: Arama yapılacak bellek bloğunun adresi.
  - `c`: Aranan karakter.
  - `n`: Arama yapılacak maksimum byte sayısı.
  - Dönüş Değeri: Bulunan karakterin adresi (s içinde), eğer karakter bulunamazsa NULL işareti.

- **ft_memcmp**: İki bellek bloğunu karşılaştırır.
  - Prototip: `int ft_memcmp(const void *s1, const void *s2, size_t n);`
  - `s1`: Karşılaştırılacak ilk bellek bloğunun adresi.
  - `s2`: Karşılaştırılacak ikinci bellek bloğunun adresi.
  - `n`: Karşılaştırılacak maksimum byte sayısı.
  - Dönüş Değeri: İlk farklı karakterin ASCII değerlerinin farkı (s1 ve s2 arasında). Eğer bloklar aynıysa 0 döner.

### Dize İşlemleri

- **ft_strlen**: Bir dizenin uzunluğunu hesaplar.
  - Prototip: `size_t ft_strlen(const char *s);`
  - `s`: Uzunluğu hesaplanacak dizi.
  - Dönüş Değeri: Dizenin uzunluğu.

- **ft_strlcpy**: Bir dizenin bir başka diziye güvenli bir şekilde kopyalanması.
  - Prototip: `size_t ft_strlcpy(char *dst, const char *src, size_t size);`
  - `dst`: Kopyalanacak dizi.
  - `src`: Kaynak dizi.
  - `size`: Kopyalanacak maksimum byte sayısı.
  - Dönüş Değeri: Kaynak dizinin uzunluğu.

- **ft_strlcat**: Bir dizenin bir başka dizeye güvenli bir şekilde eklenmesi.
  - Prototip: `size_t ft_strlcat(char *dst, const char *src, size_t size);`
  - `dst`: Dizeye eklenecek dizi.
  - `src`: Eklenen dizi.
  - `size`: Maksimum hedef dizinin boyutu.
  - Dönüş Değeri: Eklenen dizinin uzunluğu.

- **ft_strchr**: Bir karakteri bir dizide arar.
  - Prototip: `char *ft_strchr(const char *s, int c);`
  - `s`: Arama yapılacak dizi.
  - `c`: Aranan karakter.
  - Dönüş Değeri: Aranan karakterin adresi (s içinde), eğer karakter bulunamazsa NULL işareti.

- **ft_strrchr**: Bir karakteri bir dizide sondan arar.
  - Prototip: `char *ft_strrchr(const char *s, int c);`
  - `s`: Arama yapılacak dizi.
  - `c`: Aranan karakter.
  - Dönüş Değeri: Aranan karakterin sondan bulunduğu adres (s içinde), eğer karakter bulunamazsa NULL işareti.

- **ft_strnstr**: Bir alt dizenin bir dizideki pozisyonunu bulur.
  - Prototip: `char *ft_strnstr(const char *haystack, const char *needle, size_t len);`
  - `haystack`: Arama yapılacak dizi.
  - `needle`: Aranan alt dizi.
  - `len`: Arama yapılacak maksimum karakter sayısı.
  - Dönüş Değeri: Alt dizenin bulunduğu adres (haystack içinde), eğer alt dize bulunamazsa NULL işareti.

- **ft_strncmp**: İki dizeyi belirli bir sayıda karakterle karşılaştırır.
  - Prototip: `int ft_strncmp(const char *s1, const char *s2, size_t n);`
  - `s1`: Karşılaştırılacak ilk dizi.
  - `s2`: Karşılaştırılacak ikinci dizi.
  - `n`: Karşılaştırma yapılacak maksimum karakter sayısı.
  - Dönüş Değeri: Karşılaştırma sonucu, 0 (eşit), negatif (s1 < s2), pozitif (s1 > s2).

- **ft_atoi**: Bir diziyi bir tam sayıya dönüştürür.
  - Prototip: `int ft_atoi(const char *str);`
  - `str`: Dönüştürülecek dizi.
  - Dönüş Değeri: Dönüştürülen tam sayı değeri.

- **ft_itoa**: Bir tam sayıyı bir dizgiye dönüştürür.
  - Prototip: `char *ft_itoa(int n);`
  - `n`:  Dönüştürülecek tam sayı.
  - Dönüş Değeri: Dönüştürülen tam sayıyı içeren bir dizgi.

- **ft_strdup**: Bir dizinin kopyasını yapar.
  - Prototip: `char *ft_strdup(const char *s);`
  - `s`: Kopyalanacak dizi.
  - Dönüş Değeri: Yeni oluşturulan dizinin adresi.

- **ft_striteri**: Bir dizenin her karakteri üzerinde belirtilen işlemi gerçekleştirir.
  - Prototip: `void ft_striteri(char *s, void (*f)(unsigned int, char*));`
  - `s`: İşlem yapılacak dize.
  - `f`: Her karakter üzerinde çağrılacak işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_strjoin**: İki diziyi birleştirir.
  - Prototip: `char *ft_strjoin(const char *s1, const char *s2);`
  - `s1`: Birleştirilecek ilk dizi.
  - `s2`: Birleştirilecek ikinci dizi.
  - Dönüş Değeri: Yeni oluşturulan birleştirilmiş dizi.

- **ft_strmapi**: Bir dizenin her karakteri üzerinde belirtilen işlemi gerçekleştirir.
  - Prototip: `char *ft_strmapi(const char *s, char (*f)(unsigned int, char));`
  - `s`: İşlem yapılacak dize.
  - `f`: Her karakter üzerinde çağrılacak işlev.
  - Dönüş Değeri: Yeni oluşturulan dizi.

- **ft_strtrim**: Bir dizenin başındaki ve sonundaki belirli karakterleri kaldırır.
  - Prototip: `char *ft_strtrim(const char *s1, const char *set);`
  - `s1`: İşlem yapılacak dize.
  - `set`: Kaldırılacak karakter kümesi.
  - Dönüş Değeri: Yeni oluşturulan düzeltilmiş dizi.

- **ft_substr**: Bir alt dize oluşturur.
  - Prototip: `char *ft_substr(const char *s, unsigned int start, size_t len);`
  - `s`: İşlem yapılacak dize.
  - `start`: Alt dizenin başlangıç konumu.
  - `len`: Alt dizenin uzunluğu.
  - Dönüş Değeri: Yeni oluşturulan alt dizi.

- **ft_split**: Belirtilen ayırıcı karaktere göre bir dizeyi bölüp bir dize dizisi oluşturur.
  - Prototip: `char **ft_split(char const *s, char c);`
  - `s`: Bölünecek dize.
  - `c`: Ayırıcı karakter.
  - Dönüş Değeri: Oluşturulan dize dizisinin adresini içeren bir işaretçi.

- **ft_tolower**: Bir karakteri küçük harfe dönüştürür.
  - Prototip: `int ft_tolower(int c);`
  - `c`: Dönüştürülecek karakterin ASCII değeri.
  - Dönüş Değeri: Dönüştürülmüş karakterin ASCII değeri.

- **ft_toupper**: Bir karakteri büyük harfe dönüştürür.
  - Prototip: `int ft_toupper(int c);`
  - `c`: Dönüştürülecek karakterin ASCII değeri.
  - Dönüş Değeri: Dönüştürülmüş karakterin ASCII değeri.

### Karakter İşlemleri

- **ft_isalnum**: Bir karakterin alfasayısal veya sayısal olup olmadığını kontrol eder.
  - Prototip: `int ft_isalnum(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter alfasayısal veya sayısal ise 1; aksi halde 0 döner.

- **ft_isalpha**: Bir karakterin alfasayısal olup olmadığını kontrol eder.
  - Prototip: `int ft_isalpha(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter alfasayısal ise 1; aksi halde 0 döner.

- **ft_isascii**: Bir karakterin standart ASCII karakteri olup olmadığını kontrol eder.
  - Prototip: `int ft_isascii(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter standart ASCII ise 1; aksi halde 0 döner.

- **ft_isdigit**: Bir karakterin bir rakam karakteri olup olmadığını kontrol eder.
  - Prototip: `int ft_isdigit(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter bir rakam ise 1; aksi halde 0 döner.

- **ft_isprint**: Bir karakterin yazdırılabilir bir karakter olup olmadığını kontrol eder.
  - Prototip: `int ft_isprint(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter yazdırılabilir ise 1; aksi halde 0 döner.

## Bonus Fonksiyonlar
### Dosya İşlemleri

- **ft_putstr_fd**: Bir diziyi belirtilen dosya tanımlayıcısına yazar.
  - Prototip: `void ft_putstr_fd(char *s, int fd);`
  - `s`: Yazılacak dize.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_putendl_fd**: Bir diziyi belirtilen dosya tanımlayıcısına yazıp yeni bir satır ekler.
  - Prototip: `void ft_putendl_fd(char *s, int fd);`
  - `s`: Yazılacak dize.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_putnbr_fd**: Bir tam sayıyı belirtilen dosya tanımlayıcısına yazar.
  - Prototip: `void ft_putnbr_fd(int n, int fd);`
  - `n`: Yazılacak tam sayı.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_putchar_fd**: Bir karakteri belirtilen dosya tanımlayıcısına yazar.
  - Prototip: `void ft_putchar_fd(char c, int fd);`
  - `c`: Yazılacak karakter.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

### Liste işlemleri

- **ft_lstnew**: Yeni bir liste düğümü oluşturur.
  - Prototip: `t_list *ft_lstnew(void *content);`
  - `content`: Düğümün içeriği.
  - Dönüş Değeri: Oluşturulan yeni düğümün adresini içeren bir işaretçi (t_list *).

- **ft_lstadd_front**: Başa bir düğüm ekler.
  - Prototip: `void ft_lstadd_front(t_list **lst, t_list *new);`
  - `lst`: Düğümün ekleneceği liste.
  - `new`: Eklenecek düğüm.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_lstsize**: Listenin eleman sayısını döndürür.
  - Prototip: `int ft_lstsize(t_list *lst);`
  - `lst`: Boyutu hesaplanacak liste.
  - Dönüş Değeri: Listenin eleman sayısı (int).

- **ft_lstlast**: Listenin son elemanını döndürür.
  - Prototip: `t_list *ft_lstlast(t_list *lst);`
  - `lst`: Son elemanın bulunacağı liste.
  - Dönüş Değeri: Listenin son elemanının adresini içeren bir işaretçi (t_list *).

- **ft_lstadd_back**: Sona bir düğüm ekler.
  - Prototip: `void ft_lstadd_back(t_list **lst, t_list *new);`
  - `lst`: Düğümün ekleneceği liste.
  - `new`: Eklenecek düğüm.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_lstdelone**: Belirli bir düğümü siler.
  - Prototip: `void ft_lstdelone(t_list *lst, void (*del)(void*));`
  - `lst`: Silinecek düğüm.
  - `del`: Düğüm içeriğini silen işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_lstclear**: Tüm listeyi siler.
  - Prototip: `void ft_lstclear(t_list **lst, void (*del)(void*));`
  - `lst`: Silinecek liste.
  - `del`: Düğüm içeriğini silen işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_lstiter**: Bir fonksiyonu her liste elemanı için çağırır.
  - Prototip: `void ft_lstiter(t_list *lst, void (*f)(void*));`
  - `lst`: İşlem yapılacak liste.
  - `f`: Her düğüm için çağrılacak işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

- **ft_lstmap**: Bir fonksiyonu her liste elemanı için çağırır ve yeni bir liste oluşturur.
  - Prototip: `t_list *ft_lstmap(t_list *lst, void *(*f)(void*), void (*del)(void*));`
  - `lst`: Kaynak liste.
  - `f`: Her düğüm için çağrılacak işlev.
  - `del`: Düğüm içeriğini silen işlev.
  - Dönüş Değeri: Yeni oluşturulan liste başının adresini içeren bir işaretçi (t_list *).

## Notlar

### Bellek İşlemleri Nedir?
<p align="left">
Bu işlevler, genellikle bellek alanının manipülasyonu ve işlenmesi gereken durumlarda kullanılır. Örneğin, bir dizi içinde belirli bir değerin aranması, bellek alanının belirli bir değerle doldurulması veya bellek bloklarının karşılaştırılması gibi işlemlerde bu fonksiyonlara ihtiyaç duyulur.
</p>

### Dize İşlemleri Nedir?
<p align="left">
Dize işlemleri, metinsel verilerin manipülasyonu ve işlenmesi için kullanılan işlevlerdir. Bu işlevler, bir dizenin uzunluğunu hesaplamak, başka bir dizeye kopyalamak, bir dizeye yeni karakterler eklemek, belirli bir karakteri bir dizide aramak, alt dize aramak veya iki dizeyi karşılaştırmak gibi çeşitli işlemleri gerçekleştirir.
</p>

### Dosya İşlemleri Nedir?
<p align="left">
Dosya işlemleri, bir bilgisayar sistemindeki dosyalara erişmek ve bu dosyaları okumak, yazmak, oluşturmak, silmek veya değiştirmek için yapılan işlemleri ifade eder. Bu işlemler, genellikle dosyaların veri okuma ve yazma işlemlerini içerir ve dosya sistemine erişim sağlamak için kullanılır. Dosya işlemleri, programların verileri kalıcı olarak depolamak ve gerektiğinde erişmek için dosyaları kullanmasına olanak tanır.
</p>

### Karakter İşlemleri Nedir?
<p align="left">
Karakter işlemleri, genellikle bir karakterin belirli bir özelliğe sahip olup olmadığını kontrol etmek için kullanılan işlemlerdir. Örneğin, bir karakterin bir harf olup olmadığını, bir rakam olup olmadığını, bir yazdırılabilir karakter olup olmadığını veya bir ASCII karakteri olup olmadığını belirlemek gibi işlemleri içerir. Bu tür işlemler, genellikle karakter dizilerini veya kullanıcıdan alınan girdileri işlerken karakterlerin özelliklerini kontrol etmek için kullanılır.
</p>

### Liste İşlemleri Nedir?
<p align="left">
Liste işlemleri, verilerin düğüm adı verilen birimler halinde organize edilmesi ve işlenmesi için kullanılan işlevlerdir. Bu işlevler, bir veri yapısında yeni bir düğüm oluşturmak, düğüm eklemek, düğüm silmek, düğüm aramak, düğüm sayısını hesaplamak gibi çeşitli işlemleri gerçekleştirir.
</p>

### Open Fonksiyonu Nedir? 
<p align="left">
open fonksiyonu, dosya sisteminden belirtilen dosyayı açmak için kullanılan bir POSIX işlevidir. Bu işlev, bir dosyanın okunması, yazılması veya hem okunup hem yazılması gibi farklı modlarda açılmasını sağlar. Dosya zaten açıksa var olan dosyayı çağırır. örnek kod:
</p>

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("dosya.txt", O_RDONLY);
    if (fd == -1) {
        perror("Dosya açma hatası");
        return 1;
    }
    printf("Dosya başarıyla açıldı. Dosya Tanımlayıcı: %d\n", fd);

    if (close(fd) == -1) {
        perror("Dosya kapatma hatası");
        return 1;
    }
    printf("Dosya başarıyla kapatıldı.\n");

    return 0;
}
```
Open onksiyonunda kullanılabilecek bayraklar şunlardır:

- `O_RDONLY`: dosyanın salt okunur modda (read-only) açılmasını sağlayan bir işlem bayrağıdır.
- `O_WRONLY`: Dosyanın sadece yazma modunda açılmasını sağlar.
- `O_RDWR`: Dosyanın okuma ve yazma modunda açılmasını sağlar.
- `O_CREAT`: Dosya yoksa oluşturulmasını sağlar.
- `O_APPEND`: Dosyanın sonuna veri eklemeyi sağlar.
- `O_TRUNC`: Dosyanın içeriğini sıfırlar (keser).
- `O_EXCL`: Dosya varsa O_CREAT ile hata döndürür.
Bu bayraklar `|` operatörüyle birleştirilerek aynı anda birden fazla bayrağın kullanılmasını sağlar. Örneğin, `O_RDONLY | O_CREAT` şeklinde kullanılabilir.

