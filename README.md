<!-- Proje İlişkin Başlık -->
<h1 align="center">42 - Libft</h1>

<!-- Proje Açıklaması -->
<p align="center">
  `libft`, standart C kütüphanesindeki bazı temel işlevlerin nasıl çalıştığını anlamak için bir fırsat sunar. Genellikle, bu işlevleri yeniden uygulamak ve kendi kütüphanenizi oluşturmak istenen temel bir alıştırma olarak kullanılır. Bu işlevler, bellek işlemleri, dize manipülasyonu, karakter işlemleri ve listeler gibi çeşitli alanlara yayılmıştır.
</p>

<!-- Proje Logosu veya Görseli -->
<p align="center">
  <a target="blank"><img src="https://i.hizliresim.com/ffa3w9y.png" height="150" width="150" /></a>
</p>

<!-- Proje Başlıkları ve İçindekiler -->
## İçindekiler

- [Gereksinimler](#gereksinimler)
- [Kullanım](#kullanım)
- [Fonksiyonlar](#fonksiyonlar)
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

Örnek Kod:
```c
void	*ft_memset(void *s, int c, size_t n)
{
	unsigned char	*str;

	str = (unsigned char *)s;
	while (n > 0)
	{
		*str = (unsigned char)c;
		str++;
		n--;
	}
	return (s);
}
```
<p align="left">
Açıklama: s adresindeki bellek bloğunu n bayt boyunca c değeriyle doldurur. İşlev, her doldurma işleminden sonra bellek bloğunun sonraki baytına geçer ve işlem n bayt doldurulana kadar devam eder. Sonunda, fonksiyon s adresine işaret eden bir işaretçi döndürür.
</p>

- **ft_bzero**: Belleği sıfırlar.
  - Prototip: `void ft_bzero(void *s, size_t n);`
  - `s`: Sıfırlanacak bellek bloğunun başlangıç adresi.
  - `n`: Sıfırlanacak byte sayısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_bzero(void *s, size_t n)
{
	ft_memset(s, 0, n);
}
```
<p align="left">
Açıklama: ft_memset işlevini çağırır ve bu işlev aracılığıyla bellek bloğunu 0 ile doldurur. Yani, ft_bzero aslında ft_memset fonksiyonunu çağırmakla görevlidir. 
</p>

- **ft_calloc**: Belirtilen boyutta bellek bloğu tahsis eder ve sıfırlar.
  - Prototip: `void *ft_calloc(size_t count, size_t size);`
  - `count`: Tahsis edilecek öğe sayısı.
  - `size`: Her öğenin boyutu (byte cinsinden).
  - Dönüş Değeri: Tahsis edilen bellek bloğunun başlangıç adresini içeren bir işaretçi.

Örnek Kod:
```c
void	*ft_calloc(size_t count, size_t size)
{
	void	*ptr;

	ptr = malloc(size * count);
	if (!(ptr))
		return (NULL);
	ft_bzero(ptr, (count * size));
	return (ptr);
}
```
<p align="left">
Açıklama: Belirtilen boyutta bir bellek bloğu tahsis eder ve tüm alanlarını sıfırlar. Öncelikle, malloc fonksiyonuyla bellek tahsis edilir. Ardından, tahsis edilen belleğin tüm alanları ft_bzero fonksiyonu ile sıfırla doldurulur ve başlangıç adresi döndürülür.
</p>

- **ft_memcpy**: Bellek bloğunu kopyalar.
  - Prototip: `void *ft_memcpy(void *dest, const void *src, size_t n);`
  - `dest`: Kopyalanan verinin hedef adresi.
  - `src`: Kopyalanan verinin kaynak adresi.
  - `n`: Kopyalanacak byte sayısı.
  - Dönüş Değeri: Hedef adresi içeren bir işaretçi (dest).

Örnek Kod:
```c
void	*ft_memcpy(void *dst, const void *src, size_t n)
{
	size_t	i;

	if (!dst && !src)
		return (0);
	i = 0;
	while (i < n)
	{
		((unsigned char *)dst)[i] = ((unsigned char *)src)[i];
		i++;
	}
	return (dst);
}
```
<p align="left">
Açıklama: İlk olarak, hedef (dst) ve kaynak (src) bellek bloklarının adresleri ve kopyalanacak byte sayısı (n) alınır. Ardından, src bloğundaki her bir byte, dst bloğuna kopyalanır. Son olarak, dst bloğunun adresi döndürülür. Bu fonksiyonda öncekilerden farklı olarak
</p>

Not : Bu fonksiyonda öncekilerden farklı olarak type casting(tür dönüşümü) bulunmakta [Notlar](#notlar) kısmından type casting ile ilgili daha fazla bilgi edinebilirsiniz.

- **ft_memmove**: Bellek bloğunu güvenli bir şekilde kopyalar.
  - Prototip: `void *ft_memmove(void *dest, const void *src, size_t n);`
  - `dest`: Kopyalanan verinin hedef adresi.
  - `src`: Kopyalanan verinin kaynak adresi.
  - `n`: Kopyalanacak byte sayısı.
  - Dönüş Değeri: Hedef adresi içeren bir işaretçi (dest).

Örnek Kod:
```c
void	*ft_memmove(void *dst, const void *src, size_t n)
{
	if (!dst && !src)
		return (NULL);
	if (dst < src)
		ft_memcpy(dst, src, n);
	else if (dst > src)
	{
		while (n--)
			*((unsigned char *)(dst + n)) = *((unsigned char *)(src + n));
	}
	return (dst);
}
```
<p align="left">
Bu fonksiyon, bir bellek bloğunu güvenli bir şekilde taşımak için kullanılır. Yani, src adresinden n kadar bellek alanını dst adresine kopyalar veya taşır. Ancak, bu fonksiyon dst ve src adreslerinin çakışmasına izin verir; yani, kopyalama işlemi sırasında hedef ve kaynak adresler arasında çakışma olabilir. Bu durumda, memcpy fonksiyonundan farklı olarak, memmove fonksiyonu daha güvenli bir kopyalama sağlar.
dst ve src adreslerinin konumlarına göre kopyalama işlemi gerçekleştirilir:
<ul>Eğer dst kaynak adresinden daha küçükse, bellek bloğu memcpy fonksiyonu kullanılarak kopyalanır.</ul>
<ul>Eğer dst hedef adresinden daha büyükse, bellek bloğu geriye doğru (src adresinden dst adresine doğru) kopyalanır. </ul>

Not: Bu kodda overlap durumunun önüne geçmek için tersten kopyalama yapılmıştır. [Notlar](#notlar) kısmından overlap durumu ile ilgili daha fazla bilgi edinebilirsiniz.
</p>

- **ft_memchr**: Belirli bir karakteri bellekte arar.
  - Prototip: `void *ft_memchr(const void *s, int c, size_t n);`
  - `s`: Arama yapılacak bellek bloğunun adresi.
  - `c`: Aranan karakter.
  - `n`: Arama yapılacak maksimum byte sayısı.
  - Dönüş Değeri: Bulunan karakterin adresi (s içinde), eğer karakter bulunamazsa NULL işareti.

Örnek Kod:
```c
void	*ft_memchr(const void *s, int c, size_t n)
{
	const unsigned char	*str;

	str = s;
	while (n > 0)
	{
		if (*str == (unsigned char) c)
			return ((void *)str);
		n--;
		str++;
	}
	return (NULL);
}
```
<p align="left">
Bu fonksiyon, bellek bloğunda n byte boyunca dolaşarak c karakterini arar. Her bir byte üzerinde dolaşırken, aranan karakter bulunursa, bulunan karakterin adresini döndürür. Eğer karakter bulunamazsa NULL işaretini döndürür.
</p>

- **ft_memcmp**: İki bellek bloğunu karşılaştırır.
  - Prototip: `int ft_memcmp(const void *s1, const void *s2, size_t n);`
  - `s1`: Karşılaştırılacak ilk bellek bloğunun adresi.
  - `s2`: Karşılaştırılacak ikinci bellek bloğunun adresi.
  - `n`: Karşılaştırılacak maksimum byte sayısı.
  - Dönüş Değeri: İlk farklı karakterin ASCII değerlerinin farkı (s1 ve s2 arasında). Eğer bloklar aynıysa 0 döner.

Örnek Kod:
```c
int	ft_memcmp(const void *s1, const void *s2, size_t n)
{
	const unsigned char	*s1_uc;
	const unsigned char	*s2_uc;
	size_t				index;

	index = 0;
	s1_uc = (const unsigned char *)s1;
	s2_uc = (const unsigned char *)s2;
	while (index < n)
	{
		if (s1_uc[index] != s2_uc[index])
			return (s1_uc[index] - s2_uc[index]);
		index++;
	}
	return (0);
}
```
<p align="left">
Bu fonksiyon iki bellek bloğunu byte olarak karşılaştırır. İki bellek bloğunun karşılaştırılması sırasında, bellek bloklarındaki her bir byte'ın değeri diğer bellek bloğundaki karşılık gelen byte'ın değeriyle karşılaştırılır. Eğer iki byte birbirinden farklıysa, bu iki byte'nin farkını döndürür. Eğer tüm byte'lar eşit ise, 0 değerini döndürür. Bu şekilde, bellek bloklarının içeriğinin tam olarak aynı olup olmadığına göre karşılaştırma yapar.
</p>

### Dize İşlemleri

- **ft_strlen**: Bir dizenin uzunluğunu hesaplar.
  - Prototip: `size_t ft_strlen(const char *s);`
  - `s`: Uzunluğu hesaplanacak dizi.
  - Dönüş Değeri: Dizenin uzunluğu.

Örnek Kod:
```c
size_t	ft_strlen(const char *s)
{
	int	leng;
	int	i;

	i = 0;
	leng = 0;
	while (s[i] != '\0')
	{
		leng++;
		i++;
	}
	return (leng);
}
```
<p align="left">
Bu fonksiyon, verilen bir dizinin uzunluğunu hesaplar. Dizi içerisindeki karakterlerin her birini dolaşarak, dizinin sonunda '\0' (NULL) karakterini bulana kadar karakter sayısını hesaplar ve bu sayıyı döndürür.
</p>

- **ft_strlcpy**: Bir dizenin bir başka diziye güvenli bir şekilde kopyalanması.
  - Prototip: `size_t ft_strlcpy(char *dst, const char *src, size_t size);`
  - `dst`: Kopyalanacak dizi.
  - `src`: Kaynak dizi.
  - `size`: Kopyalanacak maksimum byte sayısı.
  - Dönüş Değeri: Kaynak dizinin uzunluğu.

Örnek Kod:
```c
size_t	ft_strlcpy(char *dst, const char *src, size_t size)
{
	size_t	counter;

	counter = 0;
	if (size > 0)
	{
		while ((size - 1) > counter && src[counter])
		{
			dst[counter] = src[counter];
			counter++;
		}
		dst[counter] = '\0';
	}
	while (src[counter])
		counter++;
	return (counter);
}
```
<p align="left">
Bu fonksiyon, bir kaynak dizinin içeriğini, belirtilen hedef diziye, belirtilen boyutta kopyalar. Ancak, kopyalama işlemi, hedef dizinin kapasitesini aşmaması için belirli bir boyut sınırlamasına tabidir. Kopyalama işlemi sırasında, kaynak dizideki karakterler hedef diziye kopyalanır ve sonuna '\0' (NULL) karakteri eklenerek dizinin sonlandırılması sağlanır. Son olarak, kaynak dizinin toplam uzunluğu hesaplanarak döndürülür.
</p>

- **ft_strlcat**: Bir dizenin bir başka dizeye güvenli bir şekilde eklenmesi.
  - Prototip: `size_t ft_strlcat(char *dst, const char *src, size_t size);`
  - `dst`: Dizeye eklenecek dizi.
  - `src`: Eklenen dizi.
  - `size`: Maksimum hedef dizinin boyutu.
  - Dönüş Değeri: Eklenen dizinin uzunluğu.

Örnek Kod:
```c
size_t	ft_strlcat(char *dest, const char *src, size_t size)
{
	size_t	leng;
	size_t	counter;

	counter = 0;
	leng = ft_strlen(dest);
	if (size - 1 > leng && size > 0)
	{
		while (src[counter] != '\0' && size - 1 > leng + counter)
		{
			dest[counter + leng] = src[counter];
			counter++;
		}
		dest[leng + counter] = 0;
	}
	if (leng >= size)
		leng = size;
	return (leng + ft_strlen(src));
}
```
<p align="left">
Bu fonksiyon, bir hedef diziye (dest) bir kaynak dizinin (src) içeriğini eklemek için kullanılır. Ancak, hedef dizinin belirli bir boyutunu (size) aşmaması için kontrol edilir. Fonksiyon, hedef dizinin içeriğini ölçer (leng) ve hedef dizinin mevcut uzunluğu ile eklemek istenen kaynak dizinin uzunluğunu karşılaştırır. Eğer hedef dizinin boyutu kaynak dizinin eklenmesi gereken boyuta yetmiyorsa ve hedef dizinin boyutu 0'dan büyükse, eklemeye devam edilir. Eklenen kaynak dizisi sonlandırıcı karakteri ('\0') ile bitirilir ve son olarak hedef dizinin uzunluğu geri döndürülür.
</p>

- **ft_strchr**: Bir karakteri bir dizide arar.
  - Prototip: `char *ft_strchr(const char *s, int c);`
  - `s`: Arama yapılacak dizi.
  - `c`: Aranan karakter.
  - Dönüş Değeri: Aranan karakterin adresi (s içinde), eğer karakter bulunamazsa NULL işareti.

Örnek Kod:
```c
char	*ft_strchr(const char *s, int c)
{
	while ((char)c != *s)
	{
		if (*s == 0)
			return (0);
		s++;
	}
	return ((char *)s);
}
```
<p align="left">
Bu kod, bir karakter dizisinde belirli bir karakterin ilk bulunduğu konumu bulmak için kullanılır. Karakter dizisi üzerinde dolaşarak, belirli karakteri bulduğunda bulunduğu konumu işaret eden bir adres döndürür. Eğer belirli karakter bulunmazsa, NULL değeri döndürür.
</p>

- **ft_strrchr**: Bir karakteri bir dizide sondan arar.
  - Prototip: `char *ft_strrchr(const char *s, int c);`
  - `s`: Arama yapılacak dizi.
  - `c`: Aranan karakter.
  - Dönüş Değeri: Aranan karakterin sondan bulunduğu adres (s içinde), eğer karakter bulunamazsa NULL işareti.

Örnek Kod:
```c
char	*ft_strrchr(const char *s, int c)
{
	int		i;

	i = ft_strlen(s);
	while (i >= 0)
	{
		if (s[i] == (unsigned char)c)
			return ((char *)s + i);
		i--;
	}
	return (NULL);
}
```
<p align="left">
Bu fonksiyon, bir karakter dizisinde (s) sağdan sola doğru bir karakter arar. Karakter dizisi içindeki son bulunan belirli bir karakterin adresini döndürür. Eğer karakter bulunamazsa NULL değeri döner.
</p>

- **ft_strnstr**: Bir alt dizenin bir dizideki pozisyonunu bulur.
  - Prototip: `char *ft_strnstr(const char *haystack, const char *needle, size_t len);`
  - `haystack`: Arama yapılacak dizi.
  - `needle`: Aranan alt dizi.
  - `len`: Arama yapılacak maksimum karakter sayısı.
  - Dönüş Değeri: Alt dizenin bulunduğu adres (haystack içinde), eğer alt dize bulunamazsa NULL işareti.

Örnek Kod:
```c
char	*ft_strnstr(const char *haystack, const char *needle, size_t len)
{
	const char	*h;
	const char	*n;
	size_t		counter;

	if (!needle[0])
		return ((char *)haystack);
	while (*haystack && len > 0)
	{
		h = haystack;
		n = needle;
		counter = 0;
		while (n[counter] == h[counter] && n[counter] && len - counter > 0)
			counter++;
		if (n[counter] == '\0')
			return ((char *) haystack);
		len--;
		haystack++;
	}
	return (NULL);
}
```
<p align="left">
Bu kod, bir ana dizede (haystack) belirli bir alt dizenin (needle) ilk bulunduğu konumu aramak için kullanılır. İki dize arasında dolaşarak, alt dizenin ilk karakterini bulduğunda, alt dizenin tamamının ana dizede bulunup bulunmadığını kontrol eder. Eğer alt dize bulunursa, bulunduğu konumu işaret eden bir adres döndürür. Eğer alt dize bulunmazsa veya aramaya devam edilecek karakter sayısı (len) sıfıra ulaşırsa, NULL değeri döndürür.
</p>

- **ft_strncmp**: İki dizeyi belirli bir sayıda karakterle karşılaştırır.
  - Prototip: `int ft_strncmp(const char *s1, const char *s2, size_t n);`
  - `s1`: Karşılaştırılacak ilk dizi.
  - `s2`: Karşılaştırılacak ikinci dizi.
  - `n`: Karşılaştırma yapılacak maksimum karakter sayısı.
  - Dönüş Değeri: Karşılaştırma sonucu, 0 (eşit), negatif (s1 < s2), pozitif (s1 > s2).

Örnek Kod:
```c
int	ft_strncmp(const char *s1, const char *s2, size_t size)
{
	size_t	i;

	i = 0;
	while (i < size && (s1[i] != '\0' || s2[i] != '\0'))
	{
		if (s1[i] != s2[i])
			return ((unsigned char)s1[i] - (unsigned char)s2[i]);
		i++;
	}
	return (0);
}
```
<p align="left">
Bu fonksiyon, iki dizeyi belirli bir boyutta karşılaştırır. İki dize arasında karakter karşılaştırması yapar ve eşit olmayan bir karakter bulduğunda, bu karakterlerin ASCII değerlerinin farkını döndürür. Eğer iki dize belirtilen boyutta aynıysa, yani hiçbir karakter farklı değilse veya boyut sınırına ulaşılırsa, 0 değerini döndürür.
</p>

- **ft_atoi**: Bir diziyi bir tam sayıya dönüştürür.
  - Prototip: `int ft_atoi(const char *str);`
  - `str`: Dönüştürülecek dizi.
  - Dönüş Değeri: Dönüştürülen tam sayı değeri.

Örnek Kod:
```c
int	ft_atoi(const char *str)
{
	int	i;
	int	sign;
	int	container;

	i = 0;
	sign = 1;
	container = 0;
	while (str[i] == 32 || (str[i] >= 9 && str[i] <= 13))
		i++;
	if (str[i] == '-' || str[i] == '+')
	{
		if (str[i] == '-')
			sign *= -1;
		i++;
	}
	while (str[i])
	{
		if (!(ft_isdigit(str[i])))
			return (container * sign);
		else
			container = container * 10 + (const char ) str[i] - 48;
		i++;
	}
	return (container * sign);
}
```
<p align="left">
Bu fonksiyon, bir karakter dizisini (string) tam sayıya dönüştürür. Dizideki karakterleri taramak suretiyle sayısal değeri bulur ve bu değeri döndürür. Fonksiyon, boşlukları ve tab karakterlerini (ASCII değerleri 9 ile 13 arasındaki karakterler) görmezden gelir. Eğer dize başında negatif (-) veya pozitif (+) işareti varsa, bunu dikkate alarak dönüşü yapar. Ancak, dize içerisindeki karakterlerin bir sayıyı ifade etmediği durumda (örneğin, bir harf ya da özel karakter), dönüşüme son verir ve o ana kadar elde edilen değeri döndürür.
</p>

- **ft_itoa**: Bir tam sayıyı bir dizgiye dönüştürür.
  - Prototip: `char *ft_itoa(int n);`
  - `n`:  Dönüştürülecek tam sayı.
  - Dönüş Değeri: Dönüştürülen tam sayıyı içeren bir dizgi.

Örnek Kod:
```c
static int	ft_string_leng(int num)
{
	int	i;

	if (num == 0)
		return (1);
	i = 0;
	while (num > 0 || num < 0)
	{
		num /= 10;
		i++;
	}
	return (i);
}

char	*ft_itoa(int n)
{
	int		len;
	char	*str;
	long	nbr;

	nbr = n;
	len = ft_string_leng(nbr);
	if (n < 0)
	{
		len++;
		nbr *= -1;
	}
	str = malloc(sizeof(char) * len + 1);
	if (!str)
		return (NULL);
	str[len] = '\0';
	while (nbr > 0)
	{
		str[--len] = (nbr % 10) + 48;
		nbr /= 10;
	}
	if (n < 0)
		str[0] = '-';
	if (n == 0)
		str[0] = '0';
	return (str);
}
```
<p align="left">
Bu fonksiyon, bir tamsayıyı karakter dizisine (string) dönüştürür. İlk olarak, tamsayının uzunluğunu belirlemek için ft_string_leng fonksiyonunu kullanır. Daha sonra, tamsayının negatif olup olmadığını kontrol eder ve gerektiğinde işaret karakterini ekler. Ardından, karakter dizisi için gerekli bellek alanını (malloc) ayırır. Tamsayının her basamağını sağdan sola doğru dönüştürerek karakter dizisine ekler. Son olarak, oluşturulan karakter dizisini döndürür.
</p>

Not : Bu fonksiyonda öncekilerden farklı olarak static bir fonksiyon bulunmakta [Notlar](#notlar) kısmından static fonksiyon ile ilgili daha fazla bilgi edinebilirsiniz.

- **ft_strdup**: Bir dizinin kopyasını yapar.
  - Prototip: `char *ft_strdup(const char *s);`
  - `s`: Kopyalanacak dizi.
  - Dönüş Değeri: Yeni oluşturulan dizinin adresi.

Örnek Kod:
```c
char	*ft_strdup(const char *s)
{
	char	*str;
	size_t	leng;
	size_t	i;

	leng = ft_strlen(s);
	str = (char *)malloc(sizeof(char) * (leng + 1));
	if (!(str))
		return (NULL);
	i = 0;
	while (s[i] != '\0')
	{
		str[i] = s[i];
		i++;
	}
	str[i] = '\0';
	return (str);
}
```
<p align="left">
Bu fonksiyon, bir karakter dizisinin (s) bellekte yeni bir alan tahsis ederek kopyasını oluşturur ve bu kopyanın adresini döndürür. Bellek tahsis etme işlemi malloc fonksiyonu ile yapılır. Ardından, karakter dizisinin uzunluğu hesaplanır ve bu uzunluk kadar bellekte yer ayrılır. Dizideki her karakter kopyalanarak yeni bellek bloğuna yerleştirilir. Son olarak, yeni dizinin sonuna null karakter ('\0') eklenir ve bu diziye ait adres döndürülür. Eğer bellek tahsis işlemi başarısız olursa (malloc NULL döndürürse), fonksiyon da NULL döndürür.
</p>

- **ft_striteri**: Bir dizenin her karakteri üzerinde belirtilen işlemi gerçekleştirir.
  - Prototip: `void ft_striteri(char *s, void (*f)(unsigned int, char*));`
  - `s`: İşlem yapılacak dize.
  - `f`: Her karakter üzerinde çağrılacak işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_striteri(char *s, void (*f)(unsigned int, char*))
{
	unsigned int	i;

	i = 0;
	while (s[i])
	{
		f(i, &s[i]);
		i++;
	}
	return ;
}
```
<p align="left">
Bu fonksiyon, bir karakter dizisindeki her karakter üzerinde belirtilen işlemi gerçekleştirir. İşlem, her karakterin konumu ve adresi üzerinde bir işlevin çağrılmasıyla gerçekleştirilir. Fonksiyon, karakter dizisinin her bir elemanını işlemek için bir döngü kullanır. Döngü her adımda işlevi (f) çağırarak karakterin dizideki konumunu ve adresini ileterek işlemi gerçekleştirir. Bu işlem, karakter dizisinin sonuna kadar devam eder.
</p>

örnek olarak dışarıdan yazdırma fonksiyonu ve bir string girelim.

```c
#include <stdio.h>
#include "libft.h"

void	print_char(unsigned int index, char *c) {
    printf("%c", *c);
}

int main() {
    char str[] = "Hello, World!";
    
    printf("Printing characters in the string:\n");
    ft_striteri(str, &print_char);
    putchar('\n');
    
    return 0;
}
```
<p align="left">
mainde bir string oluşturduk (str) yukarıda da yazdırma fonksiyonumuz var (print_char), ft_striteri fonksiyonuna stringimizi (str) ve yazdırma fonksiyonumuzu (print_char) yolladık ve while koşulu sağlandığı sürece yazdırma fonksiyonuna stringin indexlerini teker teker gönderip yazdırıp indexini arttırıcaktır.
</p>

- **ft_strjoin**: İki diziyi birleştirir.
  - Prototip: `char *ft_strjoin(const char *s1, const char *s2);`
  - `s1`: Birleştirilecek ilk dizi.
  - `s2`: Birleştirilecek ikinci dizi.
  - Dönüş Değeri: Yeni oluşturulan birleştirilmiş dizi.

Örnek Kod:
```c
char	*ft_strjoin(char const *s1, char const *s2)
{
	char			*str;
	unsigned int	leng;
	unsigned int	i;

	i = 0;
	if (!s1 || !s2)
		return (NULL);
	leng = ft_strlen(s1) + ft_strlen(s2);
	str = malloc(sizeof(char) * (leng + 1));
	if (!str)
		return (NULL);
	while (*s1)
	{
		str[i] = *s1++;
		i++;
	}
	while (*s2)
	{
		str[i] = *s2++;
		i++;
	}
	str[i] = '\0';
	return (str);
}
```
<p align="left">
Bu fonksiyon, verilen iki dizgiyi birleştirerek yeni bir dizi oluşturur. İlk olarak, birleştirilecek dizgilerin uzunlukları hesaplanır. Daha sonra, toplam uzunluk kadar bellek tahsis edilir ve bu belleğe ilk dizgi kopyalanır. Ardından, ikinci dizgi de kopyalanır ve sonuna '\0' (NULL karakteri) eklenerek yeni birleştirilmiş dizgi oluşturulur. Oluşturulan bu yeni dizgi bellek bloğunun adresi ile geri döndürülür. Eğer gerekli bellek tahsis edilemezse veya herhangi bir dizi NULL ise, NULL değeri döndürülür.
</p>

- **ft_strmapi**: Bir dizenin her karakteri üzerinde belirtilen işlemi gerçekleştirir.
  - Prototip: `char *ft_strmapi(const char *s, char (*f)(unsigned int, char));`
  - `s`: İşlem yapılacak dize.
  - `f`: Her karakter üzerinde çağrılacak işlev.
  - Dönüş Değeri: Yeni oluşturulan dizi.

Örnek Kod:
```c
char	*ft_strmapi(char const *s, char (*f)(unsigned int, char))
{
	char			*str;
	unsigned int	i;

	if (!s)
		return (NULL);
	str = (char *)malloc(ft_strlen(s) + 1);
	if (!str)
		return (NULL);
	i = 0;
	while (s[i] != '\0')
	{
		str[i] = f(i, s[i]);
		i++;
	}
	str[i] = '\0';
	return (str);
}
```
<p align="left">
Bu fonksiyon, verilen bir girdi dizgisinde her bir karakter üzerinde belirli bir işlemi gerçekleştiren ve sonucunu yeni bir diziye yerleştiren işlevi ifade eder. Fonksiyon, iki parametre alır: birinci parametre, işlem yapılacak olan giriş dizgisidir; ikinci parametre ise, işlemin nasıl gerçekleştirileceğini belirleyen bir işlev göstericisidir. İşlev, giriş dizgisi üzerinde döngü kullanarak her bir karakter için belirtilen işlevi çağırır ve işlevin dönüş değerlerini yeni bir diziye yerleştirir. Son olarak, işlenmiş dizgi, işlevin sonucu olarak döndürülür. Eğer giriş dizgisi NULL ise veya bellek tahsis edilemezse, NULL dönüş değeri verilir.
</p>

- **ft_strtrim**: Bir dizenin başındaki ve sonundaki belirli karakterleri kaldırır.
  - Prototip: `char *ft_strtrim(const char *s1, const char *set);`
  - `s1`: İşlem yapılacak dize.
  - `set`: Kaldırılacak karakter kümesi.
  - Dönüş Değeri: Yeni oluşturulan düzeltilmiş dizi.

Örnek Kod:
```c
static int	ft_checkset(char c, char const *set)
{
	size_t	i;

	i = 0;
	while (set[i])
	{
		if (set[i++] == c)
			return (1);
	}
	return (0);
}

char	*ft_strtrim(char const *s1, char const *set)
{
	char	*m;
	size_t	start;
	size_t	end;
	size_t	i;

	if (!s1 || !set)
		return (NULL);
	start = 0;
	end = ft_strlen(s1);
	while (s1[start] && ft_checkset(s1[start], set))
		start++;
	while (end > start && ft_checkset(s1[end - 1], set))
		end--;
	m = (char *)malloc(sizeof(char) * (end - start) + 1);
	if (!m)
		return (NULL);
	i = 0;
	while (start < end)
		m[i++] = s1[start++];
	m[i] = '\0';
	return (m);
}
```
<p align="left">
Bu fonksiyon, başında veya sonunda belirli bir karakter kümesi bulunan bir dizeden bu karakterleri kaldıran bir işlemi gerçekleştirir. İlk parametre olan s1, işlem yapılacak olan giriş dizgisidir. İkinci parametre olan set, kaldırılacak karakter kümesini belirtir. Fonksiyon, giriş dizgisinin başından ve sonundan belirtilen karakter kümesini kaldırır ve sonucu yeni bir diziye yerleştirir. Ardından, bu yeni dizi işlevin dönüş değeri olarak döndürülür.
</p>
<p align="left">
İlk olarak, giriş dizgisinin başındaki ve sonundaki karakter kümesi geçen kısımlar tespit edilir ve bu bölgelerin başlangıç ve bitiş indeksleri hesaplanır. Sonrasında, başlangıç ve bitiş indeksleri arasındaki kısmı kopyalamak için bellek tahsis edilir ve bu kısmın içine giriş dizgisinin sadece istenilen kısımları kopyalanır. Son olarak, yeni dizi oluşturulur ve işlenmiş dizgi bu diziye kopyalanır. Eğer giriş dizgisi veya karakter kümesi NULL ise, NULL dönüş değeri verilir.
</p>

- **ft_substr**: Bir alt dize oluşturur.
  - Prototip: `char *ft_substr(const char *s, unsigned int start, size_t len);`
  - `s`: İşlem yapılacak dize.
  - `start`: Alt dizenin başlangıç konumu.
  - `len`: Alt dizenin uzunluğu.
  - Dönüş Değeri: Yeni oluşturulan alt dizi.

Örnek Kod:
```c
char	*ft_substr(char const *s, unsigned int start, size_t len)
{
	size_t	i;
	size_t	j;
	char	*final;

	if (s)
	{
		if (start >= ft_strlen(s) || len == 0 || ft_strlen(s) == 0)
			return (ft_strdup(""));
		i = 0;
		while (i < len && s[i + start] != '\0')
			i++;
		final = (char *) malloc((sizeof(char) * i) + 1);
		if (!(final))
			return (NULL);
		j = 0;
		while (j < i)
		{
			final[j] = s[start + j];
			j++;
		}
		final[j] = '\0';
		return (final);
	}
	return (NULL);
}
```
<p align="left">
Bu fonksiyon, verilen bir başlangıç indeksi ve uzunluk değeriyle bir dizeden yeni bir alt dize oluşturur. İlk parametre olan s, işlem yapılacak olan giriş dizgisidir. İkinci parametre olan start, oluşturulacak alt dizinin başlangıç indeksini belirtir. Üçüncü parametre olan len, oluşturulacak alt dizenin uzunluğunu belirtir.
</p>
<p align="left">
Fonksiyon, başlangıç indeksinden başlayarak belirtilen uzunlukta olan karakterleri içeren yeni bir diziyi oluşturur. Eğer başlangıç indeksi geçerli değilse veya belirtilen uzunlukta karakter bulunmuyorsa veya giriş dizisi NULL ise, boş bir dize döndürülür.
</p>
<p align="left">
İlk olarak, giriş dizisinin uzunluğu kontrol edilir ve başlangıç indeksi uygun bir aralıkta mı diye kontrol edilir. Sonrasında, belirtilen uzunluktaki karakterleri içerecek kadar bellek tahsis edilir ve bu karakterler yeni diziye kopyalanır. Son olarak, oluşturulan alt dizeyi içeren yeni dizi dönüş değeri olarak verilir. Eğer giriş dizisi NULL ise, NULL dönüş değeri verilir.
</p>

- **ft_split**: Belirtilen ayırıcı karaktere göre bir dizeyi bölüp bir dize dizisi oluşturur.
  - Prototip: `char **ft_split(char const *s, char c);`
  - `s`: Bölünecek dize.
  - `c`: Ayırıcı karakter.
  - Dönüş Değeri: Oluşturulan dize dizisinin adresini içeren bir işaretçi.

Örnek Kod:
```c
static unsigned int	ft_word_counter(const char *s, char control)
{
	unsigned int	word;

	word = 0;
	while (*s)
	{
		if (*s == control)
			s++;
		else
		{
			while (*s != control && *s)
				s++;
			word++;
		}
	}
	return (word);
}

static unsigned int	ft_charlen(const char *s, char c)
{
	unsigned int	i;

	i = 0;
	while (s[i] && s[i] != c)
		i++;
	return (i);
}

char	**free_all(char **result)
{
	int	i;

	i = 0;
	while (result[i])
	{
		free(result[i]);
		i++;
	}
	free(result);
	return (NULL);
}

char	**ft_split(char const *s, char c)
{
	char			**arr;
	unsigned int	j;
	unsigned int	a;

	arr = (char **)malloc((ft_word_counter(s, c) + 1) * sizeof(char *));
	if (!arr)
		return (NULL);
	a = -1;
	while (*s)
	{
		while (*s == c)
			s++;
		if (*s)
		{
			arr[++a] = (char *)malloc((ft_charlen(s, c) + 1) * sizeof(char));
			if (!arr[a])
				return (free_all(arr));
			j = 0;
			while (*s && *s != c)
				arr[a][j++] = *s++;
			arr[a][j] = '\0';
		}
	}
	arr[++a] = NULL;
	return (arr);
}
```
<p align="left">
Bu kod, verilen bir dizedeki kelimeleri belirli bir ayırıcı karaktere göre parçalara ayıran ft_split fonksiyonunu gerçekleştirir.

- **ft_word_counter**: Bu fonksiyon, verilen bir dizedeki kelime sayısını belirler. Dize üzerinde dolaşarak ayırıcı karakteri geçer ve her kelimeyi bulurken kelime sayısını artırır.

- **ft_charlen**: Belirli bir karaktere kadar olan karakterlerin uzunluğunu hesaplar. Dizge içinde belirli bir karaktere kadar olan karakter sayısını bulur.

- **free_all**: Bellekte dinamik olarak tahsis edilen belleği serbest bırakmak için kullanılır. Bu fonksiyon, ft_split fonksiyonu içinde bellek tahsis edilirken oluşabilecek hataları kontrol etmek için çağrılır.

- **ft_split**: Ana fonksiyon, verilen bir dizedeki kelimeleri belirtilen ayırıcı karaktere göre parçalara böler. Bellekte parçaları tutmak için gerekli alanı tahsis eder ve ardından dizeyi ayırırken bu alanı doldurur. Son olarak, parçaları içeren bir dizi döndürür.
</p>
<p align="left">
Yani kısaca, bir dizedeki kelimeleri belirli bir ayırıcı karaktere göre parçalara böler. Dize içindeki her kelimeyi ayrıştırır ve ayrıca bellekte her bir kelime için ayrılan hafızayı serbest bırakır. Son olarak, parçalanmış kelimeleri içeren bir dizi döndürür.
</p>

- **ft_tolower**: Bir karakteri küçük harfe dönüştürür.
  - Prototip: `int ft_tolower(int c);`
  - `c`: Dönüştürülecek karakterin ASCII değeri.
  - Dönüş Değeri: Dönüştürülmüş karakterin ASCII değeri.

Örnek Kod:
```c
int	ft_tolower(int c)
{
	if (c >= 65 && c <= 90)
		return (c + 32);
	return (c);
}
```
<p align="left">
Bu kod, verilen bir karakteri küçük harfe dönüştürmek için kullanılır. Fonksiyon, verilen karakterin ASCII değerini kontrol eder. Eğer verilen karakter büyük bir harfse (ASCII değeri 65 ile 90 arasında ise), küçük harfe dönüştürmek için ASCII değerine 32 ekler. Aksi halde, karakteri olduğu gibi geri döndürür. Bu işlem sonucunda dönüştürülen karakterin ASCII değeri, küçük harfe karşılık gelen ASCII değeri olur.
</p>

- **ft_toupper**: Bir karakteri büyük harfe dönüştürür.
  - Prototip: `int ft_toupper(int c);`
  - `c`: Dönüştürülecek karakterin ASCII değeri.
  - Dönüş Değeri: Dönüştürülmüş karakterin ASCII değeri.

Örnek Kod:
```c
int	ft_toupper(int c)
{
	if (c >= 'a' && c <= 'z')
		return (c - 32);
	return (c);
}
```
<p align="left">
Bu kod, verilen bir karakteri büyük harfe dönüştürmek için kullanılır. Fonksiyon, verilen karakterin ASCII değerini kontrol eder. Eğer verilen karakter küçük bir harfse (ASCII değeri 'a' ile 'z' arasında ise), büyük harfe dönüştürmek için ASCII değerinden 32 çıkarır. Aksi halde, karakteri olduğu gibi geri döndürür. Bu işlem sonucunda dönüştürülen karakterin ASCII değeri, büyük harfe karşılık gelen ASCII değeri olur.
</p>

### Karakter İşlemleri

- **ft_isalnum**: Bir karakterin alfasayısal veya sayısal olup olmadığını kontrol eder.
  - Prototip: `int ft_isalnum(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter alfasayısal veya sayısal ise 1; aksi halde 0 döner.

Örnek Kod:
```c
int	ft_isalnum(int c)
{
	return (ft_isalpha(c) || ft_isdigit(c));
}
```
<p align="left">

Bu kod, verilen bir karakterin alfasayısal (harf veya rakam) olup olmadığını kontrol eder. ft_isalpha ve ft_isdigit fonksiyonlarını kullanarak, verilen karakterin hem bir harf hem de bir rakam olup olmadığını kontrol eder. Eğer verilen karakter bir harf ise veya bir rakamsa, fonksiyon 1 değerini döndürür (doğru). Aksi halde, 0 değerini döndürür (yanlış). Bu sayede, verilen karakterin alfasayısal olup olmadığını belirlemek için kullanılabilir.
</p>

- **ft_isalpha**: Bir karakterin alfasayısal olup olmadığını kontrol eder.
  - Prototip: `int ft_isalpha(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter alfasayısal ise 1; aksi halde 0 döner.

Örnek Kod:
```c
int	ft_isalpha(int c)
{
	return ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z'));
}
```
<p align="left">
Bu kod, verilen bir karakterin bir alfabetik karakter olup olmadığını kontrol eder. Karakterin 'a' ile 'z' arasında veya 'A' ile 'Z' arasında olup olmadığını kontrol eder. Eğer verilen karakter alfabede bir harf ise, fonksiyon 1 değerini döndürür (doğru). Aksi halde, 0 değerini döndürür (yanlış). Bu sayede, verilen karakterin alfabede bir harf olup olmadığını belirlemek için kullanılabilir.
</p>

- **ft_isascii**: Bir karakterin standart ASCII karakteri olup olmadığını kontrol eder.
  - Prototip: `int ft_isascii(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter standart ASCII ise 1; aksi halde 0 döner.

Örnek Kod:
```c
int	ft_isascii(int c)
{
	return (c >= 0 && c < 128);
}
```
<p align="left">
Bu kod, verilen bir karakterin ASCII karakter setine ait olup olmadığını kontrol eder. ASCII karakter setindeki karakterler 0 ile 127 arasında yer alır. Dolayısıyla, bu fonksiyon, verilen karakterin 0 (dahil) ile 127 (hariç) arasında olup olmadığını kontrol eder. Eğer karakter ASCII karakter setine aitse, yani 0 ile 127 arasında bir değerse, fonksiyon 1 değerini döndürür (doğru). Aksi halde, 0 değerini döndürür (yanlış). Bu fonksiyon, bir karakterin ASCII karakter setine ait olup olmadığını belirlemek için kullanılabilir.
</p>

- **ft_isdigit**: Bir karakterin bir rakam karakteri olup olmadığını kontrol eder.
  - Prototip: `int ft_isdigit(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter bir rakam ise 1; aksi halde 0 döner.

Örnek Kod:
```c
int	ft_isdigit(int c)
{
	return (c <= '9' && c >= '0');
}
```
<p align="left">
Bu fonksiyon, verilen bir karakterin bir rakam karakteri olup olmadığını kontrol eder. Rakam karakterleri '0' ile '9' arasında ASCII kodlarına sahiptir. Dolayısıyla, bu fonksiyon verilen karakterin bu aralıkta olup olmadığını kontrol eder. Eğer verilen karakter bir rakam karakteri ise, fonksiyon doğru (1) değerini döndürür. Aksi takdirde, yanlış (0) değerini döndürür. Bu fonksiyon, bir karakterin rakam olup olmadığını belirlemek için kullanılır.
</p>

- **ft_isprint**: Bir karakterin yazdırılabilir bir karakter olup olmadığını kontrol eder.
  - Prototip: `int ft_isprint(int c);`
  - `c`: Kontrol edilecek karakterin ASCII değeri.
  - Dönüş Değeri: Eğer karakter yazdırılabilir ise 1; aksi halde 0 döner.

Örnek Kod:
```c
int	ft_isprint(int c)
{
	return (c >= 32 && c <= 126);
}
```
<p align="left">
Bu fonksiyon, verilen bir karakterin basılabilir (printable) karakter olup olmadığını kontrol eder. Basılabilir karakterler ASCII kod 32 ile 126 arasındadır ve klavye üzerinde yazdırılabilir karakterlerin çoğunu temsil eder. Fonksiyon, verilen karakterin bu aralıkta olup olmadığını kontrol eder. Eğer verilen karakter bir basılabilir karakter ise, fonksiyon doğru (1) değerini döndürür. Aksi takdirde, yanlış (0) değerini döndürür. Bu fonksiyon, bir karakterin ekrana yazdırılabilir olup olmadığını kontrol etmek için kullanılır.
</p>

## Bonus Fonksiyonlar
### Dosya İşlemleri

- **ft_putstr_fd**: Bir diziyi belirtilen dosya tanımlayıcısına yazar.
  - Prototip: `void ft_putstr_fd(char *s, int fd);`
  - `s`: Yazılacak dize.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_putstr_fd(char *s, int fd)
{
	int	i;

	i = 0;
	while (s[i])
	{
		ft_putchar_fd(s[i], fd);
		i++;
	}
	return ;
}
```
<p align="left">
Bu fonksiyon, verilen bir karakter dizisini (string) belirtilen dosya tanımlayıcısına (fd) yazdırmak için kullanılır. Karakter dizisi s üzerinde döngü kullanarak her bir karakteri tek tek ft_putchar_fd fonksiyonu aracılığıyla belirtilen dosya tanımlayıcısına yazdırır. Sonuç olarak, bu fonksiyon verilen karakter dizisini belirtilen dosya tanımlayıcısına yazdırır.
</p>

- **ft_putendl_fd**: Bir diziyi belirtilen dosya tanımlayıcısına yazıp yeni bir satır ekler.
  - Prototip: `void ft_putendl_fd(char *s, int fd);`
  - `s`: Yazılacak dize.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_putendl_fd(char *s, int fd)
{
	if (s)
	{
		ft_putstr_fd(s, fd);
		ft_putchar_fd('\n', fd);
	}
}
```
<p align="left">
Bu fonksiyon, verilen bir karakter dizisini (s) belirtilen dosya tanımlayıcısına (fd) yazdırmak için kullanılır. Ancak yazdırma işleminden sonra bir satır sonu karakteri (\n) ekleyerek yeni bir satır oluşturur. Fonksiyon, verilen karakter dizisinin boş olup olmadığını kontrol eder ve eğer boş değilse önce ft_putstr_fd fonksiyonuyla karakter dizisini yazdırır, ardından bir satır sonu karakteri ekler. Sonuç olarak, bu fonksiyon belirtilen karakter dizisini belirtilen dosya tanımlayıcısına yazdırır ve ardından bir satır sonu karakteri ekler.
</p>

- **ft_putnbr_fd**: Bir tam sayıyı belirtilen dosya tanımlayıcısına yazar.
  - Prototip: `void ft_putnbr_fd(int n, int fd);`
  - `n`: Yazılacak tam sayı.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_putnbr_fd(int n, int fd)
{
	long int	nb;
	char		c;

	if (fd < 0)
		return ;
	nb = n;
	if (nb < 0)
	{
		write (fd, "-", 1);
		nb *= -1;
	}
	if (nb < 10)
	{
		c = nb + '0';
		write(fd, &c, 1);
	}
	else
	{
		ft_putnbr_fd((nb / 10), fd);
		c = nb % 10 + '0';
		write(fd, &c, 1);
	}
}
```
<p align="left">
Bu fonksiyon, bir tamsayıyı (n) belirtilen dosya tanımlayıcısına (fd) yazdırmak için kullanılır. Fonksiyon, öncelikle tamsayının negatif olup olmadığını kontrol eder. Eğer negatifse, negatif işaretini yazdırır ve sayıyı pozitife dönüştürür. Daha sonra, sayının basamaklarını ayrı ayrı yazdırmak için bir döngü kullanır. Her basamak için, sayıyı 10'a böler ve kalanını ASCII karakterine dönüştürerek yazdırır. Bu işlem, sayının her basamağı için tekrarlanır ve sonunda tamsayı, belirtilen dosya tanımlayıcısına doğru biçimde yazdırılmış olur.
</p>

- **ft_putchar_fd**: Bir karakteri belirtilen dosya tanımlayıcısına yazar.
  - Prototip: `void ft_putchar_fd(char c, int fd);`
  - `c`: Yazılacak karakter.
  - `fd`: Yazma işleminin yapılacağı dosya tanımlayıcısı.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_putchar_fd(char c, int fd)
{
	write(fd, &c, 1);
}
```
<p align="left">
Bu fonksiyon, bir karakteri (c) belirtilen dosya tanımlayıcısına (fd) yazdırmak için kullanılır. write fonksiyonu kullanılarak karakter belirtilen dosya tanımlayıcısına yazdırılır. Burada &c ifadesi, karakterin bellek adresine işaret eder ve 1 ise yazdırılacak byte sayısını temsil eder. Bu durumda, sadece bir karakterin yazdırılacağı belirtilmiştir.
</p>

### Liste işlemleri

- **ft_lstnew**: Yeni bir liste düğümü oluşturur.
  - Prototip: `t_list *ft_lstnew(void *content);`
  - `content`: Düğümün içeriği.
  - Dönüş Değeri: Oluşturulan yeni düğümün adresini içeren bir işaretçi (t_list *).

Örnek Kod:
```c
t_list	*ft_lstnew(void *content)
{
	t_list	*new_list;

	new_list = malloc(sizeof(t_list));
	if (!new_list)
		return (NULL);
	new_list->content = content;
	new_list->next = NULL;
	return (new_list);
}
```
<p align="left">

</p>

- **ft_lstadd_front**: Başa bir düğüm ekler.
  - Prototip: `void ft_lstadd_front(t_list **lst, t_list *new);`
  - `lst`: Düğümün ekleneceği liste.
  - `new`: Eklenecek düğüm.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_lstadd_front(t_list **lst, t_list *new)
{
	if (!lst && !new)
		return ;
	new->next = *lst;
	*lst = new;
}
```

- **ft_lstsize**: Listenin eleman sayısını döndürür.
  - Prototip: `int ft_lstsize(t_list *lst);`
  - `lst`: Boyutu hesaplanacak liste.
  - Dönüş Değeri: Listenin eleman sayısı (int).

Örnek Kod:
```c
int	ft_lstsize(t_list *lst)
{
	int	counter;

	counter = 0;
	while (lst)
	{
		lst = lst->next;
		counter++;
	}
	return (counter);
}
```

- **ft_lstlast**: Listenin son elemanını döndürür.
  - Prototip: `t_list *ft_lstlast(t_list *lst);`
  - `lst`: Son elemanın bulunacağı liste.
  - Dönüş Değeri: Listenin son elemanının adresini içeren bir işaretçi (t_list *).

Örnek Kod:
```c
t_list	*ft_lstlast(t_list *lst)
{
	if (!lst)
		return (0);
	while (lst->next != NULL)
	{
		lst = lst->next;
	}
	return (lst);
}
```
<p align="left">

</p>

- **ft_lstadd_back**: Sona bir düğüm ekler.
  - Prototip: `void ft_lstadd_back(t_list **lst, t_list *new);`
  - `lst`: Düğümün ekleneceği liste.
  - `new`: Eklenecek düğüm.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_lstadd_back(t_list **lst, t_list *new)
{
	t_list	*last;

	if (*lst)
	{
		last = ft_lstlast(*lst);
		last->next = new;
	}
	else
		*lst = new;
}
```

- **ft_lstdelone**: Belirli bir düğümü siler.
  - Prototip: `void ft_lstdelone(t_list *lst, void (*del)(void*));`
  - `lst`: Silinecek düğüm.
  - `del`: Düğüm içeriğini silen işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_lstdelone(t_list *lst, void (*del)(void*))
{
	if (!lst)
		return ;
	del(lst->content);
	free(lst);
}
```
<p align="left">
Bu fonksiyon, bir t_list düğümünü ve içeriğini silen işlevdir. İlk parametre olarak aldığı t_list düğümünün içeriğini ikinci parametre olarak aldığı silme işleviyle siler. Sonrasında düğümü ve içeriğini bellekten serbest bırakır.
</p>

- **ft_lstclear**: Tüm listeyi siler.
  - Prototip: `void ft_lstclear(t_list **lst, void (*del)(void*));`
  - `lst`: Silinecek liste.
  - `del`: Düğüm içeriğini silen işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_lstclear(t_list **lst, void (*del)(void*))
{
	t_list	*clear;

	clear = *lst;
	while (lst && *lst)
	{
		clear = (*lst)->next;
		ft_lstdelone(*lst, del);
		*lst = clear;
	}
}
```
<p align="left">

</p>

- **ft_lstiter**: Bir fonksiyonu her liste elemanı için çağırır.
  - Prototip: `void ft_lstiter(t_list *lst, void (*f)(void*));`
  - `lst`: İşlem yapılacak liste.
  - `f`: Her düğüm için çağrılacak işlev.
  - Dönüş Değeri: Yok (void). Sadece işlemi gerçekleştirir.

Örnek Kod:
```c
void	ft_lstiter(t_list *lst, void (*f)(void *))
{
	while (lst)
	{
		f(lst->content);
		lst = lst->next;
	}
}
```
<p align="left">

</p>

- **ft_lstmap**: Bir fonksiyonu her liste elemanı için çağırır ve yeni bir liste oluşturur.
  - Prototip: `t_list *ft_lstmap(t_list *lst, void *(*f)(void*), void (*del)(void*));`
  - `lst`: Kaynak liste.
  - `f`: Her düğüm için çağrılacak işlev.
  - `del`: Düğüm içeriğini silen işlev.
  - Dönüş Değeri: Yeni oluşturulan liste başının adresini içeren bir işaretçi (t_list *).

Örnek Kod:
```c
t_list	*ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
{
	t_list	*new;
	t_list	*begin;
	void	*content;

	if (lst == NULL || f == NULL)
		return (NULL);
	begin = NULL;
	while (lst)
	{
		content = (*f)(lst->content);
		new = ft_lstnew(content);
		if (!new)
		{
			(*del)(content);
			ft_lstclear(&begin, del);
			return (NULL);
		}
		ft_lstadd_back(&begin, new);
		lst = lst->next;
	}
	return (begin);
}
```

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

### Malloc Nedir?
<p align="left">
malloc, C programlama dilinde dinamik bellek tahsis etmek için kullanılan bir fonksiyondur. Çalışma zamanında belirli bir boyutta bellek bloğu talep etmek için kullanılır. Örnek Kod:
</p>

```c
int main() {
    // 10 integer değeri için bellek tahsis et
    int *ptr = (int *)malloc(10 * sizeof(int));

    // Bellek tahsisi başarılı mı kontrol et
    if (ptr == NULL) {
        printf("Bellek tahsis edilemedi!");
        return -1;
    }

    // Belleği kullan
    for (int i = 0; i < 10; i++) {
        ptr[i] = i * 2;
        printf("%d ", ptr[i]);
    }

    // Belleği serbest bırak
    free(ptr);

    return 0;
}
```

### Calloc Nedir?
<p align="left">
calloc, bellek tahsis etmek için kullanılan bir işlevdir. "Calloc" kelimesi "continuous allocation" kelimelerinin kısaltmasıdır. calloc, bellek tahsis etmek için malloc işlevi gibi kullanılır, ancak farklı olarak ayrılan belleği sıfırlar, yani tüm byte'ları sıfır değeriyle doldurur.
</p>

### Type Casting (Tür Dönüşümü) Nedir?
<p align="left">
Tip dönüşümü veya type casting, bir veri türünün diğerine dönüştürülmesi işlemidir. Bu işlem, bir değişkenin veri türünü değiştirmek veya bir ifade veya değerin beklenen veri türüne dönüştürmek için yapılır. Örneğin, bir tamsayıyı ondalık sayıya dönüştürmek veya bir karakter dizisini tamsayıya dönüştürmek gibi durumlar tip dönüşümü gerektirir. Tip dönüşümü, programcının veri türlerini uygun şekilde işlemesini sağlar ve veri türü uyumsuzluklarını giderir. Örnek Kod:
</p>

```c
#include <stdio.h>

int main() {
    int a = 10;
    double b;

    // int tipindeki a değişkenini double tipine dönüştürerek b'ye atadık
    b = (double)a;

    printf("a: %d\n", a);
    printf("b: %.2f\n", b);

    return 0;
}
```
### Overlap (Çakışma) Durumu Nedir?
<p align="left">
Overlap, genellikle birbirini takip eden iki nesnenin veya olayın aynı alana veya sürece denk gelmesi durumunu ifade eder. Özellikle programlama bağlamında, overlap, bellek bloklarının veya veri yapılarının aynı bellek alanında veya aynı zaman aralığında yer alması durumunu ifade eder. Bu durum, bellek hataları, veri bütünlüğü sorunları veya beklenmedik davranışlara neden olabilir. Overlap durumları genellikle programların düzeltilmesi gereken hatalarını belirtir. Örnek Kod:
</p>

```c
#include <stdio.h>

// overlap fonksiyonu, iki dizinin çakışıp çakışmadığını kontrol eder
int overlap(int arr1[], int size1, int arr2[], int size2) {
    // Birinci dizinin son elemanı ikinci dizinin ilk elemanından küçükse veya
    // ikinci dizinin son elemanı birinci dizinin ilk elemanından küçükse çakışma yoktur
    if (arr1[size1 - 1] < arr2[0] || arr2[size2 - 1] < arr1[0]) {
        return 0; // Çakışma yok
    } else {
        return 1; // Çakışma var
    }
}

int main() {
    int arr1[] = {1, 2, 3, 4, 5};
    int arr2[] = {4, 5, 6, 7, 8};
    
    int size1 = sizeof(arr1) / sizeof(arr1[0]);
    int size2 = sizeof(arr2) / sizeof(arr2[0]);

    if (overlap(arr1, size1, arr2, size2)) {
        printf("Diziler çakışıyor.\n");
    } else {
        printf("Diziler çakışmıyor.\n");
    }

    return 0;
}

```
### Static Nedir? 
<p align="left">
"static" kelimesi, bir değişkenin veya fonksiyonun programın çalışma süresi boyunca sabit bir bellek konumuna sahip olduğunu belirtmek için kullanılan bir anahtar kelimedir.
</p>
<p align="left">
Bir değişken "static" olarak tanımlandığında, bu değişken global kapsamda tanımlanır, yani tanımlandığı dosyanın dışında erişilemez. Ayrıca, "static" olarak tanımlanan bir değişkenin ömrü, programın başlangıcından sonuna kadar devam eder ve bellekteki konumu sabittir.
</p>
<p align="left">
Bir fonksiyon "static" olarak tanımlandığında, bu fonksiyon yalnızca tanımlandığı dosyanın içinde erişilebilir. Başka bir dosyadan bu fonksiyona erişilemez. Bu şekilde, fonksiyonun kapsamı sınırlanmış olur ve kodun daha modüler hale gelmesine yardımcı olur.
</p>

### size_t Nedir? 
<p align="left">
size_t, C ve C++ gibi dillerde kullanılan bir tamsayı türüdür. Bu tür, bellek adresleme ve dizi indeksleme gibi boyutları ifade etmek için genellikle kullanılır. Platforma bağlı olarak değişebilir ve genellikle en büyük adreslenebilir bellek miktarını temsil eder. Örneğin, bir dizinin boyutunu veya bir bellek bloğunun boyutunu temsil etmek için kullanılabilir. size_t, stddef.h başlık dosyasında tanımlanır.
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

