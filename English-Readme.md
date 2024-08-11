## Language Selection / Dil Seçimi

- [English](#english)
- [Türkçe](#turkish)

---

<h3 align="center">English</h3>

---

<h1 align="center">42 - Libft 📚</h1>

<!-- Project Description -->
<p align="center">
  `libft` offers an opportunity to understand how some basic functions in the standard C library work. It is often used as a fundamental exercise to reimplement these functions and create your own library. These functions span various areas such as memory operations, string manipulation, character handling, and lists.
</p>

<!-- Project Logo or Visual -->
<p align="center">
  <a target="blank"><img src="https://i.hizliresim.com/ffa3w9y.png" height="150" width="150" /></a>
</p>

---

<!-- Project Titles and Table of Contents -->
## Table of Contents 📚
- [Requirements](#requirements)
- [Usage](#usage)
- [Functions](#functions)
- [Bonus Functions](#bonus-functions)
- [Notes](#notes)
  - [What is Malloc?](#what-is-malloc) 
  - [What is Calloc?](#what-is-calloc) 
  - [What is Type Casting?](#what-is-type-casting) 
  - [What is Overlap?](#what-is-overlap) 
  - [What is Static?](#what-is-static) 
  - [What is size_t?](#what-is-size_t) 
  - [What is the Open Function?](#what-is-the-open-function) 

---

<!-- Requirements -->
## Requirements 

There are no specific requirements to run the project. You only need a C compiler (like gcc) and a terminal interface.

---

<!-- Usage -->
## Usage 

To use the project, follow these steps:

1. Click on the `<> Code` button in the upper right corner.
2. Then, click on `Download Zip` to download the zip file.
3. Extract the zip file on your computer.

---

<!-- Functions -->

<h1 align="center">Functions</h1> 

---

### Memory Operations

- **ft_memset**: Fills memory with a constant byte.
  - Prototype: `void *ft_memset(void *s, int c, size_t n);`
  - `s`: Pointer to the block of memory to fill.
  - `c`: Value to be set.
  - `n`: Number of bytes to be set to the value.
  - Return Value: A pointer to the memory area `s`.

Example Code:
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
Explanation: This function fills the first `n` bytes of the memory area pointed to by `s` with the constant byte `c`. It returns a pointer to the memory area `s`.
</p>

---

- **ft_calloc**: Allocates and resets a block of memory of the given size.
  - Prototype: `void *ft_calloc(size_t count, size_t size);`
  - `count`: The number of items to allocate.
  - `size`: The size of each item (in bytes).
  - Return Value: A pointer to the starting address of the allocated memory block.

Example Code:
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
Description: Allocates a block of memory of the specified size and resets all its areas. First, memory is allocated with the malloc function. Then, all areas of the allocated memory are zero-filled with the ft_bzero function and the starting address is returned.
</p>

---

- **ft_memcpy**: Copies a block of memory.
  - Prototype: `void *ft_memcpy(void *dest, const void *src, size_t n);`
  - `dest`: The destination address of the copied data.
  - `src`: The source address of the copied data.
  - `n`: Number of bytes to copy.
  - Return Value: A pointer (dest) containing the destination address.

Example Code:
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

---

<p align="left">
Description: First, the addresses of the destination (dst) and source (src) memory blocks and the number of bytes to copy (n) are obtained. Then, each byte in the src block is copied to the dst block. Finally, the address of the dst block is returned. This function differs from the previous ones in that
</p>

Note : This function has type casting unlike the previous ones, you can read more about type casting in [Notes](#notes).

---

- **ft_memmove**: Safely copies a block of memory.
  - Prototype: `void *ft_memmove(void *dest, const void *src, size_t n);`
  - `dest`: The destination address of the copied data.
  - `src`: The source address of the copied data.
  - `n`: Number of bytes to copy.
  - Return Value: A pointer (dest) containing the destination address.

Example Code:
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
This function is used to safely move a block of memory, meaning it copies or moves a memory area of size n from the src address to the dst address. However, this function allows the dst and src addresses to overlap; that is, there may be an overlap between the destination and source addresses during the copy operation. In this case, unlike the memcpy function, the memmove function provides a safer copy.
The copying process is performed based on the positions of the dst and src addresses:
<ul>If dst is smaller than the source address, the memory block is copied using the memcpy function.</ul>
<ul>If dst is larger than the target address, the memory block is copied backward (from the src address to the dst address).</ul>

Note: In this code, reverse copying is done to prevent overlap. You can learn more about the overlap situation in the [Notes](#notes) section.
</p>

---

- **ft_memchr**: Searches for a specific character in memory.
  - Prototype: `void *ft_memchr(const void *s, int c, size_t n);`
  - `s`: The address of the memory block where the search will be performed.
  - `c`: The character to be searched for.
  - `n`: The maximum number of bytes to search.
  - Return Value: The address of the found character (within s), or NULL if the character is not found.

Example Code:
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
This function searches for the character c within a memory block by iterating over n bytes. As it goes through each byte, if the searched character is found, it returns the address of the found character. If the character is not found, it returns NULL.
</p>

---

- **ft_memcmp**: Compares two blocks of memory.
  - Prototype: `int ft_memcmp(const void *s1, const void *s2, size_t n);`
  - `s1`: Address of the first block of memory to be compared.
  - `s2`: Address of the second block of memory to be compared.
  - `n`: Maximum number of bytes to compare.
  - Return Value: The difference of the ASCII values of the first differing character (between s1 and s2). Returns 0 if the blocks are identical.

Example Code:
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
This function compares two blocks of memory byte by byte. During the comparison of the two memory blocks, the value of each byte in one block is compared with the value of the corresponding byte in the other block. If the two bytes are different, it returns the difference between the two bytes. If all the bytes are equal, it returns 0. In this way, it performs a comparison based on whether the contents of the memory blocks are exactly the same.
</p>

---

### String Operations

- **ft_strlen**: Calculates the length of a string.
  - Prototype: `size_t ft_strlen(const char *s);`
  - `s`: The string for which the length will be calculated.
  - Return Value: The length of the string.

Example Code:
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
This function calculates the length of a given string. It traverses each character in the string and counts the number of characters until it finds the '\0' (NULL) character at the end of the string, returning this count.
</p>

---

- **ft_strlcpy**: Safely copies a string from one array to another.
  - Prototype: `size_t ft_strlcpy(char *dst, const char *src, size_t size);`
  - `dst`: The destination array where the string will be copied.
  - `src`: The source string.
  - `size`: The maximum number of bytes to copy.
  - Return Value: The length of the source string.

Example Code:
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
This function copies the contents of a source string to the specified destination array, respecting a specified size limit. However, the copying process is subject to a size restriction to ensure that it does not exceed the capacity of the destination array. During the copying process, characters from the source string are copied to the destination array, and a '\0' (NULL) character is appended to terminate the string. Finally, the total length of the source string is calculated and returned.
</p>

---

- **ft_strlcat**: Safely appends a string to another string.
  - Prototype: `size_t ft_strlcat(char *dst, const char *src, size_t size);`
  - `dst`: The destination string to which the source string will be appended.
  - `src`: The string to be appended.
  - `size`: The maximum size of the destination string.
  - Return Value: The length of the appended string.

Example Code:
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
This function is used to append the contents of a source string (src) to a destination array (dst). However, it checks to ensure that it does not exceed a specified size (size) of the destination array. The function measures the contents of the destination array (length) and compares the current length of the destination array with the length of the source string to be appended. If the size of the destination array is not sufficient for the source string to be appended and the size of the destination array is greater than 0, the appending continues. The appended source string is terminated with a null character ('\0'), and finally, the length of the destination array is returned.
</p>

---

- **ft_strchr**: Searches for a character in a string.
  - Prototype: `char *ft_strchr(const char *s, int c);`
  - `s`: The string to be searched.
  - `c`: The character to be searched for.
  - Return Value: The address of the searched character (in s), or NULL if the character is not found.

Example Code:
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
This code is used to find the first occurrence of a specific character in a string. It traverses the string and returns the address that marks the position of the character when found. If the character is not found, it returns NULL.
</p>

---

- **ft_strrchr**: Searches for a character in a string from the end.
  - Prototype: `char *ft_strrchr(const char *s, int c);`
  - `s`: The string to be searched.
  - `c`: The character to be searched for.
  - Return Value: The address of the searched character from the end (in s), or NULL if the character is not found.

Example Code:
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
This function searches for a character in a string (s) from right to left. It returns the address of the last occurrence of the specified character in the string. If the character is not found, it returns NULL.
</p>

---

- **ft_strnstr**: Finds the position of a substring within a string.
  - Prototype: `char *ft_strnstr(const char *haystack, const char *needle, size_t len);`
  - `haystack`: The string to be searched.
  - `needle`: The substring to be searched for.
  - `len`: The maximum number of characters to search.
  - Return Value: The address of the found substring (in haystack), or NULL if the substring is not found.

Example Code:
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
This code is used to search for the first occurrence of a specific substring (needle) within a main string (haystack). It traverses both strings and, when it finds the first character of the substring, checks whether the entire substring exists within the main string. If the substring is found, it returns an address marking its position. If the substring is not found, or if the number of characters remaining to search (len) reaches zero, it returns NULL.
</p>

---

- **ft_strncmp**: Compares two strings for a specified number of characters.
  - Prototype: `int ft_strncmp(const char *s1, const char *s2, size_t n);`
  - `s1`: The first string to be compared.
  - `s2`: The second string to be compared.
  - `n`: The maximum number of characters to compare.
  - Return Value: The result of the comparison; 0 (equal), negative (s1 < s2), positive (s1 > s2).

Example Code:
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
This function compares two strings for a specified size. It performs character comparisons between the two strings and returns the difference of the ASCII values of the characters when it finds a differing character. If the two strings are the same within the specified size, meaning there are no differing characters, or if the size limit is reached, it returns 0.
</p>

---

- **ft_atoi**: Converts a string to an integer.
  - Prototype: `int ft_atoi(const char *str);`
  - `str`: The string to be converted.
  - Return Value: The converted integer value.

Example Code:
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
This function converts a string to an integer. It scans the characters in the string to find the numerical value and returns this value. The function ignores whitespace and tab characters (those with ASCII values between 9 and 13). If there is a negative (-) or positive (+) sign at the beginning of the string, it takes that into account during the conversion. However, if the characters in the string do not represent a number (for example, a letter or special character), the conversion ends, and it returns the value obtained up to that point.
</p>

---

- **ft_itoa**: Converts an integer to a string.
  - Prototype: `char *ft_itoa(int n);`
  - `n`: The integer to be converted.
  - Return Value: A string containing the converted integer.

Example Code:
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
This function converts an integer to a string. It first uses the `ft_string_leng` function to determine the length of the integer. Then, it checks whether the integer is negative and adds a sign character if necessary. Next, it allocates the required memory for the character string using `malloc`. It converts each digit of the integer from right to left and appends it to the character string. Finally, it returns the created character string.
</p>

Note: Unlike previous functions, this function contains a static function. You can find more information about static functions in the [Notes](#notlar) section.

---

- **ft_strdup**: Creates a duplicate of a string.
  - Prototype: `char *ft_strdup(const char *s);`
  - `s`: The string to be copied.
  - Return Value: The address of the newly created string.

Example Code:
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
This function creates a copy of a string (s) by allocating new memory and returns the address of this copy. Memory allocation is performed using the `malloc` function. Then, the length of the string is calculated, and memory is allocated accordingly. Each character from the original string is copied to the newly allocated memory block. Finally, a null character ('\0') is added to the end of the new string, and the address of this string is returned. If the memory allocation fails (if `malloc` returns NULL), the function also returns NULL.
</p>

---

- **ft_striteri**: Applies the specified operation on each character of a string.
  - Prototype: `void ft_striteri(char *s, void (*f)(unsigned int, char*));`
  - `s`: The string on which the operation will be performed.
  - `f`: The function to be called on each character.
  - Return Value: None (void). It simply performs the operation.

Example Code:
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
This function applies the specified operation to each character in a string. The operation is performed by calling a function with the position and address of each character. The function uses a loop to process each element of the character string. In each iteration, it calls the function (f), passing the character's position and address to perform the operation. This process continues until the end of the string.
</p>

As an example, let's use an external printing function and input a string.

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
In the main function, we created a string (str) and have a printing function (print_char) defined above. We passed our string (str) and the printing function (print_char) to the `ft_striteri` function, which, as long as the while condition is satisfied, will send the indices of the string one by one to the printing function, printing them and incrementing the index.
</p>

---

- **ft_strjoin**: Joins two strings together.
  - Prototype: `char *ft_strjoin(const char *s1, const char *s2);`
  - `s1`: The first string to be joined.
  - `s2`: The second string to be joined.
  - Return Value: A newly created concatenated string.

Example Code:
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
This function creates a new string by joining the two given strings together. First, the lengths of the strings to be joined are calculated. Then, memory is allocated for the total length, and the first string is copied into this memory. Next, the second string is also copied, and a null character ('\0') is added to the end to create the new concatenated string. The address of this newly created string is returned. If the necessary memory cannot be allocated or if any of the strings is NULL, the function returns NULL.
</p>

---

- **ft_strmapi**: Applies the specified operation to each character of a string.
  - Prototype: `char *ft_strmapi(const char *s, char (*f)(unsigned int, char));`
  - `s`: The string on which the operation will be performed.
  - `f`: The function to be called on each character.
  - Return Value: A newly created string.

Example Code:
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
This function represents an operation that performs a specified action on each character of the given input string and places the result into a new string. The function takes two parameters: the first parameter is the input string on which the operation will be performed, and the second parameter is a function pointer that determines how the operation will be carried out. The function uses a loop to iterate over the input string, calling the specified function for each character and placing the return values of the function into a new string. Finally, the processed string is returned as the result of the function. If the input string is NULL or memory cannot be allocated, the function returns NULL.
</p>

---

- **ft_strtrim**: Removes specified characters from the beginning and end of a string.
  - Prototype: `char *ft_strtrim(const char *s1, const char *set);`
  - `s1`: The string on which the operation will be performed.
  - `set`: The set of characters to be removed.
  - Return Value: A newly created trimmed string.

Example Code:

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
This function performs an operation that removes a specified set of characters from the beginning or end of a string. The first parameter, `s1`, is the input string on which the operation will be performed. The second parameter, `set`, specifies the set of characters to be removed. The function removes the specified set of characters from the start and end of the input string and places the result into a new string. This new string is then returned as the function's return value.
</p>
<p align="left">
First, the sections of the input string that contain the character set at the beginning and end are identified, and the starting and ending indices of these regions are calculated. Next, memory is allocated to copy the section between the starting and ending indices, and only the desired parts of the input string are copied into this section. Finally, a new string is created, and the processed string is copied into this new string. If the input string or the character set is NULL, the function returns NULL.
</p>

---

- **ft_substr**: Creates a substring.
  - Prototype: `char *ft_substr(const char *s, unsigned int start, size_t len);`
  - `s`: The string from which the substring will be created.
  - `start`: The starting position of the substring.
  - `len`: The length of the substring.
  - Return Value: A newly created substring.

Example Code:
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
This function creates a new substring from a given string using a specified starting index and length. The first parameter, `s`, is the input string on which the operation will be performed. The second parameter, `start`, indicates the starting index of the substring to be created. The third parameter, `len`, specifies the length of the substring to be created.
</p>
<p align="left">
The function generates a new string that contains characters starting from the specified starting index for the given length. If the starting index is invalid, or if there are not enough characters for the specified length, or if the input string is NULL, an empty string is returned.
</p>
<p align="left">
First, the length of the input string is checked, and it is verified whether the starting index is within a valid range. Then, memory is allocated to hold the specified number of characters, and these characters are copied into the new string. Finally, the new string containing the created substring is returned as the function's result. If the input string is NULL, the function returns NULL.
</p>

---

- **ft_split**: Splits a string into an array of strings based on a specified delimiter character.
  - Prototype: `char **ft_split(char const *s, char c);`
  - `s`: The string to be split.
  - `c`: The delimiter character.
  - Return Value: A pointer containing the address of the created array of strings.

Example Code:
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
This code implements the ft_split function, which splits the words in a given string based on a specified delimiter character.

- **ft_word_counter**: This function determines the number of words in a given string. It traverses the string, skips the delimiter character, and increments the word count whenever it finds a word.

- **ft_charlen**: Calculates the length of characters up to a specified character. It finds the number of characters in the string up to the specified character.

- **free_all**: Used to free dynamically allocated memory. This function is called to check for errors that may occur during memory allocation in the ft_split function.

- **ft_split**: The main function that splits the words in a given string based on the specified delimiter character. It allocates the necessary space in memory to hold the parts and then fills this space while splitting the string. Finally, it returns an array containing the parts.
</p>
<p align="left">
In summary, it splits the words in a string based on a specified delimiter character. It parses each word within the string and also frees the memory allocated for each word. Ultimately, it returns an array containing the split words.
</p>

---

- **ft_tolower**: Converts a character to lowercase.
  - Prototype: `int ft_tolower(int c);`
  - `c`: ASCII value of the character to be converted.
  - Return Value: ASCII value of the converted character.

Example Code:
```c
int	ft_tolower(int c)
{
	if (c >= 65 && c <= 90)
		return (c + 32);
	return (c);
}
```

<p align="left">
This code is used to convert a given character to lowercase. The function checks the ASCII value of the provided character. If the given character is an uppercase letter (i.e., its ASCII value is between 65 and 90), it adds 32 to the ASCII value to convert it to lowercase. Otherwise, it returns the character as it is. As a result, the ASCII value of the converted character corresponds to that of the lowercase letter.
</p>

---

- **ft_toupper**: Converts a character to uppercase.
  - Prototype: `int ft_toupper(int c);`
  - `c`: The ASCII value of the character to be converted.
  - Return Value: The ASCII value of the converted character.

Example Code:
```c
int	ft_toupper(int c)
{
	if (c >= 'a' && c <= 'z')
		return (c - 32);
	return (c);
}
```

<p align="left">
This code is used to convert a given character to uppercase. The function checks the ASCII value of the provided character. If the character is a lowercase letter (i.e., its ASCII value is between 'a' and 'z'), it subtracts 32 from the ASCII value to convert it to uppercase. Otherwise, it returns the character as is. As a result of this operation, the ASCII value of the converted character corresponds to that of the uppercase letter.
</p>

---


### Character Operations

- **ft_isalnum**: Checks if a character is alphanumeric or numeric.
  - Prototype: `int ft_isalnum(int c);`
  - `c`: The ASCII value of the character to be checked.
  - Return Value: Returns 1 if the character is alphanumeric or numeric; otherwise, it returns 0.

Example Code:
```c
int	ft_isalnum(int c)
{
	return (ft_isalpha(c) || ft_isdigit(c));
}
```

<p align="left">
This code checks whether a given character is alphanumeric (letter or digit). By using the ft_isalpha and ft_isdigit functions, it verifies if the given character is either a letter or a digit. If the character is a letter or a digit, the function returns 1 (true). Otherwise, it returns 0 (false). Thus, it can be used to determine whether the given character is alphanumeric.
</p>

- **ft_isalpha**: Checks whether a character is alphabetic.
  - Prototip: `int ft_isalpha(int c);`
  - `c`: The ASCII value of the character to be checked.
  - Return Value: Returns 1 if the character is alphabetic; otherwise, it returns 0.

Example Code:
Örnek Kod:
```c
int	ft_isalpha(int c)
{
	return ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z'));
}
```

<p align="left">
This code checks whether a given character is an alphabetic character. It verifies if the character is between 'a' and 'z' or between 'A' and 'Z'. If the given character is a letter in the alphabet, the function returns 1 (true). Otherwise, it returns 0 (false). Thus, it can be used to determine whether the given character is a letter in the alphabet.
</p>

---

- **ft_isascii**: Checks whether a character is a standard ASCII character.
  - Prototype: `int ft_isascii(int c);`
  - `c`: The ASCII value of the character to be checked.
  - Return Value: Returns 1 if the character is standard ASCII; otherwise, it returns 0.

Example Code:
```c
int	ft_isascii(int c)
{
	return (c >= 0 && c < 128);
}
```

<p align="left">
This code checks whether a given character belongs to the ASCII character set. Characters in the ASCII character set range from 0 to 127. Therefore, this function checks if the given character is within the range of 0 (inclusive) to 127 (exclusive). If the character is part of the ASCII character set, meaning it has a value between 0 and 127, the function returns 1 (true). Otherwise, it returns 0 (false). This function can be used to determine if a character belongs to the ASCII character set.
</p>

---

- **ft_isdigit**: Checks if a character is a digit character.
  - Prototype: `int ft_isdigit(int c);`
  - `c`: The ASCII value of the character to be checked.
  - Return Value: Returns 1 if the character is a digit; otherwise, returns 0.

Example Code:
```c
int	ft_isdigit(int c)
{
	return (c <= '9' && c >= '0');
}
```
<p align="left">
This function checks if a given character is a digit character. Digit characters have ASCII codes between '0' and '9'. Therefore, this function checks whether the given character falls within this range. If the given character is a digit character, the function returns true (1). Otherwise, it returns false (0). This function is used to determine whether a character is a digit.
</p>

---

- **ft_isprint**: Checks if a character is a printable character.
  - Prototype: `int ft_isprint(int c);`
  - `c`: The ASCII value of the character to be checked.
  - Return Value: Returns 1 if the character is printable; otherwise, returns 0.

Example Code:
```c
int	ft_isprint(int c)
{
	return (c >= 32 && c <= 126);
}
```

<p align="left">
This function checks if a given character is a printable character. Printable characters have ASCII codes between 32 and 126, representing most of the printable characters on the keyboard. The function checks whether the given character falls within this range. If the given character is a printable character, the function returns true (1). Otherwise, it returns false (0). This function is used to determine if a character can be printed on the screen.
</p>

---

<h1 align="center">Bonus Functions</h1>

### File Operations

- **ft_putstr_fd**: Writes a string to the specified file descriptor.
  - Prototype: `void ft_putstr_fd(char *s, int fd);`
  - `s`: The string to be written.
  - `fd`: The file descriptor where the write operation will take place.
  - Return Value: None (void). Performs the operation only.

Example Code:
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
This function is used to write a given string to the specified file descriptor (fd). It iterates over each character in the string `s` and writes each character to the specified file descriptor using the `ft_putchar_fd` function. As a result, this function writes the given string to the specified file descriptor.
</p>

---

- **ft_putendl_fd**: Writes a string to the specified file descriptor and adds a new line.
  - Prototype: `void ft_putendl_fd(char *s, int fd);`
  - `s`: The string to be written.
  - `fd`: The file descriptor where the write operation will take place.
  - Return Value: None (void). Performs the operation only.

Example Code:
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
This function is used to write a given string (s) to the specified file descriptor (fd). However, it creates a new line by adding a newline character (\n) after the write operation. The function checks if the given string is not empty, and if it is not, it first writes the string using the `ft_putstr_fd` function and then adds a newline character. As a result, this function writes the specified string to the specified file descriptor and then adds a newline character.
</p>

---

- **ft_putnbr_fd**: Writes an integer to the specified file descriptor.
  - Prototype: `void ft_putnbr_fd(int n, int fd);`
  - `n`: The integer to be written.
  - `fd`: The file descriptor where the write operation will take place.
  - Return Value: None (void). Performs the operation only.

Example Code:
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
This function is used to write an integer (n) to the specified file descriptor (fd). The function first checks if the integer is negative. If it is negative, it writes the negative sign and converts the number to positive. Then, it uses a loop to write each digit of the number separately. For each digit, it divides the number by 10 and converts the remainder to its ASCII character to write it. This process is repeated for each digit of the number, and in the end, the integer is written correctly to the specified file descriptor.
</p>

---

- **ft_putchar_fd**: Writes a character to the specified file descriptor.
  - Prototype: `void ft_putchar_fd(char c, int fd);`
  - `c`: The character to be written.
  - `fd`: The file descriptor where the write operation will take place.
  - Return Value: None (void). Performs the operation only.

Example Code:
```c
void	ft_putchar_fd(char c, int fd)
{
	write(fd, &c, 1);
}
```

<p align="left">
This function is used to write a character (c) to the specified file descriptor (fd). The character is written to the specified file descriptor using the write function. Here, the &c expression points to the memory address of the character, and 1 represents the number of bytes to be written. In this case, it specifies that only one character will be written.
</p>

---

### List Operations

- **ft_lstnew**: Creates a new list node.
  - Prototype: `t_list *ft_lstnew(void *content);`
  - `content`: The content of the node.
  - Return Value: A pointer (t_list *) containing the address of the newly created node.

Example Code:
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
This function creates a new list node. The `ft_lstnew` function takes a content (`content`) and creates a new node that holds this content. The function allocates memory to create the new node, and if the allocation fails, it returns `NULL`. If the allocation is successful, the content of the node is filled with the given `content` value, and the `next` pointer is set to `NULL`, making the node ready to be added to the end of the list.
</p>

---

- **ft_lstadd_front**: Adds a node to the front.
  - Prototype: `void ft_lstadd_front(t_list **lst, t_list *new);`
  - `lst`: The list to which the node will be added.
  - `new`: The node to be added.
  - Return Value: None (void). Performs the operation only.

Example Code:
```c
void	ft_lstadd_front(t_list **lst, t_list *new)
{
	if (!lst && !new)
		return ;
	new->next = *lst;
	*lst = new;
}
```

<p align="left">
This function adds a new node to the beginning of a list. The `ft_lstadd_front` function takes a pointer to a list (`lst`) and the node to be added (`new`). If either the `lst` or `new` pointers are invalid (NULL), the function returns without performing any operation. Otherwise, the `next` pointer of the new node is set to point to the first node of the existing list, and then the list pointer (`lst`) is updated to point to the new node. This way, the new node is added to the front of the list.
</p>

---

- **ft_lstsize**: Returns the number of elements in the list.
  - Prototype: `int ft_lstsize(t_list *lst);`
  - `lst`: The list for which the size will be calculated.
  - Return Value: The number of elements in the list (int).

Example Code:
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

<p align="left">
This function returns the number of elements in a list. The `ft_lstsize` function takes a list pointer (`lst`) and uses a loop to count the elements of the list. The loop continues until the list pointer is `NULL`, and at each step, the list pointer is moved to the next node. During this process, a counter is incremented to calculate the total number of elements. When the loop is completed, the counter value is returned, representing the number of elements in the list.
</p>

---

- **ft_lstlast**: Returns the last element of the list.
  - Prototype: `t_list *ft_lstlast(t_list *lst);`
  - `lst`: The list from which the last element will be found.
  - Return Value: A pointer (t_list *) containing the address of the last element in the list.

Example Code:
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
This function returns the last element of a list. The `ft_lstlast` function takes a list pointer (`lst`) and traverses the list until it reaches the end. If the list pointer is `NULL`, the function returns `0`. If the list pointer points to a valid node, the function returns the pointer to the last node. The loop continues until the `next` pointer of the node is `NULL`, and when the last node is found, the address of that node is returned.
</p>

---

- **ft_lstadd_back**: Adds a node to the end.
  - Prototype: `void ft_lstadd_back(t_list **lst, t_list *new);`
  - `lst`: The list to which the node will be added.
  - `new`: The node to be added.
  - Return Value: None (void). Performs the operation only.

Example Code:
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

<p align="left">
This function adds a new node to the end of a list. The `ft_lstadd_back` function takes a list pointer (`lst`) and the node to be added (`new`). If the list already contains elements, the `ft_lstlast` function is used to find the last node of the list, and the `next` pointer of this node is set to point to the new node. If the list is empty (if the `*lst` pointer is `NULL`), the new node is set as the first node of the list. The function does not return any value.
</p>

---

- **ft_lstdelone**: Deletes a specific node.
  - Prototype: `void ft_lstdelone(t_list *lst, void (*del)(void*));`
  - `lst`: The node to be deleted.
  - `del`: The function that deletes the content of the node.
  - Return Value: None (void). Performs the operation only.

Example Code:
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
This function deletes a t_list node and its content. It takes the t_list node as the first parameter and uses the deletion function provided as the second parameter to delete the content of the node. Afterward, it frees the memory for the node and its content.
</p>

---

- **ft_lstclear**: Deletes the entire list.
  - Prototype: `void ft_lstclear(t_list **lst, void (*del)(void*));`
  - `lst`: The list to be deleted.
  - `del`: The function that deletes the content of the nodes.
  - Return Value: None (void). Performs the operation only.

Example Code:
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
This function deletes all nodes of a list and frees the memory. The `ft_lstclear` function takes a pointer to a list (`lst`) and a function (`del`) used to free the content of the nodes. The loop progresses from the beginning to the end of the list, calling the `ft_lstdelone` function for each node to delete it and free the memory. At each step, the current node is deleted before moving to the next node. The function does not return any value when the operation is complete.
</p>

---

- **ft_lstiter**: Calls a function for each element of the list.
  - Prototype: `void ft_lstiter(t_list *lst, void (*f)(void*));`
  - `lst`: The list to be processed.
  - `f`: The function to be called for each node.
  - Return Value: None (void). Performs the operation only.

Example Code:
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
This function applies a given function (`f`) to the content of each node in a list. The `ft_lstiter` function takes a list pointer (`lst`) and iterates through the list. At each step, the content of the current node is processed using the function `f`. The loop continues until the end of the list, and the function does not return any value when the operation is complete.
</p>

---

- **ft_lstmap**: Calls a function for each element of the list and creates a new list.
  - Prototype: `t_list *ft_lstmap(t_list *lst, void *(*f)(void*), void (*del)(void*));`
  - `lst`: The source list.
  - `f`: The function to be called for each node.
  - `del`: The function that deletes the content of the nodes.
  - Return Value: A pointer (t_list *) containing the address of the head of the newly created list.

Example Code:
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

<p align="left">
This function applies a given function (`f`) to the content of each node in a list and creates a new list with the results of that function. The `ft_lstmap` function takes a source list (`lst`), a function (`f`) to be called for each node, and a function (`del`) to be used for deleting the content of a node if an error occurs while creating a new node. The function iterates through the source list, applies the function `f` to the content of each node, and creates a new node. If a new node cannot be created, the function cleans up all the nodes in the new list and returns `NULL`. If the operation is successful, it returns a pointer to the head of the new list.
</p>

---

<h1 align="center">Notes</h1> 

---

### What are Memory Operations?
<p align="left">
These functions are typically used in situations where memory space needs to be manipulated and processed. For example, functions are required for operations such as searching for a specific value within an array, filling a memory area with a specific value, or comparing blocks of memory.
</p>

---

### What are String Operations?
<p align="left">
String operations are functions used for manipulating and processing textual data. These functions perform various operations such as calculating the length of a string, copying one string to another, adding new characters to a string, searching for a specific character in a string, searching for a substring, or comparing two strings.
</p>

---

### What are File Operations?
<p align="left">
File operations refer to the actions performed to access files in a computer system and read, write, create, delete, or modify those files. These operations typically involve reading and writing data to files and are used to access the file system. File operations allow programs to use files to store data permanently and access it when needed.
</p>

---

### What are Character Operations?
<p align="left">
Character operations are typically used to check whether a character possesses a certain property. For example, these operations may include determining whether a character is a letter, a digit, a printable character, or an ASCII character. Such operations are commonly used to check the properties of characters when processing character strings or user inputs.
</p>

---

### What are List Operations?
<p align="left">
List operations are functions used for organizing and processing data in units called nodes. These functions perform various operations such as creating a new node in a data structure, adding a node, deleting a node, searching for a node, and calculating the number of nodes.
</p>

---

### What is Malloc?
<p align="left">
malloc is a function used in the C programming language to allocate dynamic memory. It is used to request a block of memory of a specific size at runtime. Example Code:
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

---

### What is Calloc?
<p align="left">
calloc is a function used to allocate memory. The term "Calloc" is an abbreviation of "continuous allocation." It is used like the malloc function for memory allocation; however, unlike malloc, calloc initializes the allocated memory to zero, filling all bytes with the value zero.
</p>

---

### What is Type Casting?
<p align="left">
Type casting is the process of converting one data type into another. This process is done to change the data type of a variable or to convert an expression or value into the expected data type. For example, converting an integer to a floating-point number or converting a string to an integer requires type casting. Type casting allows programmers to handle data types appropriately and resolves data type mismatches. Example Code:
</p>

---

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

---

### What is Overlap?
<p align="left">
Overlap refers to the situation where two consecutive objects or events coincide in the same area or process. In the context of programming, overlap describes the condition where memory blocks or data structures occupy the same memory space or the same time interval. This situation can lead to memory errors, data integrity issues, or unexpected behaviors. Overlap situations typically indicate errors that need to be corrected in programs. Example Code:
</p>

```c
#include <stdio.h>

// The overlap function checks if two arrays overlap
int overlap(int arr1[], int size1, int arr2[], int size2) {
    // If the last element of the first array is less than the first element of the second array
    // or the last element of the second array is less than the first element of the first array, there is no overlap
    if (arr1[size1 - 1] < arr2[0] || arr2[size2 - 1] < arr1[0]) {
        return 0; // No overlap
    } else {
        return 1; // Overlap exists
    }
}

int main() {
    int arr1[] = {1, 2, 3, 4, 5};
    int arr2[] = {4, 5, 6, 7, 8};
    
    int size1 = sizeof(arr1) / sizeof(arr1[0]);
    int size2 = sizeof(arr2) / sizeof(arr2[0]);

    if (overlap(arr1, size1, arr2, size2)) {
        printf("Arrays overlap.\n");
    } else {
        printf("Arrays do not overlap.\n");
    }

    return 0;
}
```

---

### What is Static?
<p align="left">
The term "static" is a keyword used to indicate that a variable or function has a fixed memory location throughout the program's runtime.
</p>
<p align="left">
When a variable is defined as "static," it is defined with global scope, meaning it cannot be accessed outside the file in which it is defined. Additionally, a variable defined as "static" has a lifetime that continues from the start to the end of the program, and its memory location is fixed.
</p>
<p align="left">
When a function is defined as "static," it can only be accessed within the file where it is defined. This function cannot be accessed from another file. This way, the function's scope is limited, helping to make the code more modular.
</p>

---

### What is size_t?
<p align="left">
size_t is an integer type used in languages like C and C++. This type is commonly used to represent sizes, such as for memory addressing and array indexing. It can vary depending on the platform and generally represents the largest addressable amount of memory. For example, it can be used to represent the size of an array or a block of memory. size_t is defined in the stddef.h header file.
</p>

---

### What is the Open Function?
<p align="left">
The open function is a POSIX operation used to open a specified file from the file system. This function allows a file to be opened in different modes, such as for reading, writing, or both. If the file is already open, it will refer to the existing file. Here is an example code:
</p>

---

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("file.txt", O_RDONLY);
    if (fd == -1) {
        perror("File opening error");
        return 1;
    }
    printf("File opened successfully. File Descriptor: %d\n", fd);

    if (close(fd) == -1) {
        perror("File closing error");
        return 1;
    }
    printf("File closed successfully.\n");

    return 0;
}
```

### Flags for the `open` Function

The following flags can be used with the `open` function:

- `O_RDONLY`: A flag that allows the file to be opened in read-only mode.
- `O_WRONLY`: A flag that allows the file to be opened in write-only mode.
- `O_RDWR`: A flag that allows the file to be opened in both read and write mode.
- `O_CREAT`: A flag that creates the file if it does not exist.
- `O_APPEND`: A flag that allows data to be appended to the end of the file.
- `O_TRUNC`: A flag that truncates the file, clearing its contents.
- `O_EXCL`: A flag that causes an error to be returned when using `O_CREAT` if the file already exists.

These flags can be combined using the `|` operator to use multiple flags simultaneously. For example, it can be used as `O_RDONLY | O_CREAT`.

---

<h3 align="center">Türkçe</h3>

---


<!-- Proje İlişkin Başlık -->
<h1 align="center">42 - Libft 📚</h1>

<!-- Proje Açıklaması -->
<p align="center">
  `libft`, standart C kütüphanesindeki bazı temel işlevlerin nasıl çalıştığını anlamak için bir fırsat sunar. Genellikle, bu işlevleri yeniden uygulamak ve kendi kütüphanenizi oluşturmak istenen temel bir alıştırma olarak kullanılır. Bu işlevler, bellek işlemleri, dize manipülasyonu, karakter işlemleri ve listeler gibi çeşitli alanlara yayılmıştır.
</p>

<!-- Proje Logosu veya Görseli -->
<p align="center">
  <a target="blank"><img src="https://i.hizliresim.com/ffa3w9y.png" height="150" width="150" /></a>
</p>

<!-- Proje Başlıkları ve İçindekiler -->
## İçindekiler 📚
- [Gereksinimler](#gereksinimler)
- [Kullanım](#kullanım)
- [Fonksiyonlar](#fonksiyonlar)
- [Bonus Fonksiyonlar](#bonus-fonksiyonlar)
- [Notlar](#notlar)
  - [Malloc Nedir?](#malloc-nedir) 
  - [Calloc Nedir?](#calloc-nedir) 
  - [Type Casting (Tür Dönüşümü) Nedir?](#type-casting-tür-dönüşümü-nedir) 
  - [Overlap (Çakışma) Durumu Nedir?](#overlap-çakışma-durumu-nedir) 
  - [Static Nedir?](#static-nedir) 
  - [size_t Nedir?](#size_t-nedir) 
  - [Open Fonksiyonu Nedir?](#open-fonksiyonu-nedir) 

---

<!-- Gereksinimler -->
## Gereksinimler 

Projeyi çalıştırmak için herhangi bir özel gereksinim yoktur. Sadece C derleyicisine (gcc gibi) ve bir terminal arayüzüne ihtiyacınız vardır.

---
<!-- Kullanım -->
## Kullanım 

Projeyi kullanmak için aşağıdaki adımları izleyebilirsiniz:

1. Sağ Üstteki `<> Code` kısmına tıklayın.
2. Daha sonra `Download Zip` kısmına tıklayın ve zip dosyasını indirin.
3. Bilgisayarınızdaki zip dosyasını açın.

---

<!-- Fonksiyonlar -->

<h1 align="center">Fonksiyonlar</h1> 

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

<h1 align="center">Bonus Fonksiyonlar</h1> 

---

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

---

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

---

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

---

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

---

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
Bu fonksiyon, yeni bir liste düğümü oluşturur. `ft_lstnew` fonksiyonu, bir içerik (`content`) alır ve bu içeriği tutan yeni bir düğüm oluşturur. Fonksiyon, yeni düğümü oluşturmak için bellek tahsisi yapar ve eğer tahsis başarılı olmazsa, `NULL` döner. Tahsis başarılı olursa, düğümün içeriği verilen `content` değeri ile doldurulur ve `next` işaretçisi `NULL` olarak ayarlanır, böylece düğüm, listenin sonuna eklenmeye hazır hale gelir.
</p>

---

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

<p align="left">
Bu fonksiyon, bir listenin başına yeni bir düğüm ekler. `ft_lstadd_front` fonksiyonu, bir listenin işaretçisini (`lst`) ve eklenmek istenen düğümü (`new`) alır. Eğer `lst` veya `new` işaretçileri geçersizse (NULL), fonksiyon hiçbir işlem yapmadan döner. Aksi halde, yeni düğümün `next` işaretçisi mevcut listenin ilk düğümünü gösterecek şekilde ayarlanır ve ardından liste işaretçisi (`lst`), yeni düğümü gösterecek şekilde güncellenir. Böylece, yeni düğüm listenin başına eklenmiş olur.
</p>

---

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

<p align="left">
Bu fonksiyon, bir listenin eleman sayısını döndürür. `ft_lstsize` fonksiyonu, bir liste işaretçisini (`lst`) alır ve listenin elemanlarını saymak için bir döngü kullanır. Döngü, liste işaretçisi `NULL` olana kadar devam eder ve her adımda liste işaretçisi bir sonraki düğüme kaydırılır. Bu sırada bir sayaç (`counter`) artırılarak toplam eleman sayısı hesaplanır. Döngü tamamlandığında, sayaç değeri döndürülür ve bu değer, listenin eleman sayısını temsil eder.
</p>

---

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
Bu fonksiyon, bir listenin son elemanını döndürür. `ft_lstlast` fonksiyonu, bir liste işaretçisini (`lst`) alır ve listenin sonuna ulaşana kadar listeyi ilerletir. Eğer liste işaretçisi `NULL` ise, fonksiyon `0` döner. Liste işaretçisi geçerli bir düğümü gösteriyorsa, fonksiyon, son düğümün işaretçisini döner. Döngü, düğümün `next` işaretçisi `NULL` olana kadar devam eder ve son düğüm bulunduğunda, bu düğümün adresi döndürülür.
</p>

---

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

<p align="left">
Bu fonksiyon, bir listenin sonuna yeni bir düğüm ekler. `ft_lstadd_back` fonksiyonu, bir liste işaretçisini (`lst`) ve eklenmek istenen düğümü (`new`) alır. Eğer liste zaten eleman içeriyorsa, `ft_lstlast` fonksiyonu kullanılarak listenin son düğümü bulunur ve bu düğümün `next` işaretçisi yeni düğümü gösterecek şekilde ayarlanır. Eğer liste boşsa (`*lst` işaretçisi `NULL` ise), yeni düğüm doğrudan listenin ilk düğümü olarak ayarlanır. Fonksiyon herhangi bir değer döndürmez.
</p>

---

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

---

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
Bu fonksiyon, bir listenin tüm düğümlerini siler ve belleği serbest bırakır. `ft_lstclear` fonksiyonu, bir liste işaretçisini (`lst`) ve düğüm içeriğini serbest bırakmak için kullanılan bir işlevi (`del`) alır. Döngü, listenin başından sonuna kadar ilerler, her düğüm için `ft_lstdelone` fonksiyonunu çağırarak düğümü siler ve belleği serbest bırakır. Her adımda, bir sonraki düğüme geçmeden önce mevcut düğüm silinir. Fonksiyon, işlem tamamlandığında hiçbir değer döndürmez.
</p>

---

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
Bu fonksiyon, verilen bir işlevi (`f`), bir listedeki her düğümün içeriği üzerinde uygular. `ft_lstiter` fonksiyonu, bir liste işaretçisini (`lst`) alır ve liste boyunca iterasyon yapar. Her adımda, mevcut düğümün içeriği (`content`) işlev `f` kullanılarak işlenir. Döngü, listenin sonuna kadar devam eder ve işlem tamamlandığında hiçbir değer döndürmez.
</p>

---

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
<p align="left">
Bu fonksiyon, verilen bir işlevi (`f`) bir listedeki her düğümün içeriği üzerinde uygular ve bu işlevin sonucuyla yeni bir liste oluşturur. `ft_lstmap` fonksiyonu, bir kaynak liste (`lst`), her düğüm için çağrılacak bir işlev (`f`), ve eğer bir düğüm oluşturulurken hata oluşursa, düğüm içeriğini silmek için kullanılacak bir işlev (`del`) alır. Fonksiyon, kaynak liste boyunca iterasyon yapar, her düğümün içeriği üzerinde işlev `f`'i uygular ve yeni bir düğüm oluşturur. Eğer yeni bir düğüm oluşturulamazsa, fonksiyon, yeni listenin tüm düğümlerini temizler ve `NULL` döner. İşlem başarılı olursa, yeni listenin başının işaretçisini döndürür.
</p>

---

<h1 align="center">Notlar</h1> 

---

### Bellek İşlemleri Nedir?
<p align="left">
Bu işlevler, genellikle bellek alanının manipülasyonu ve işlenmesi gereken durumlarda kullanılır. Örneğin, bir dizi içinde belirli bir değerin aranması, bellek alanının belirli bir değerle doldurulması veya bellek bloklarının karşılaştırılması gibi işlemlerde bu fonksiyonlara ihtiyaç duyulur.
</p>

---

### Dize İşlemleri Nedir?
<p align="left">
Dize işlemleri, metinsel verilerin manipülasyonu ve işlenmesi için kullanılan işlevlerdir. Bu işlevler, bir dizenin uzunluğunu hesaplamak, başka bir dizeye kopyalamak, bir dizeye yeni karakterler eklemek, belirli bir karakteri bir dizide aramak, alt dize aramak veya iki dizeyi karşılaştırmak gibi çeşitli işlemleri gerçekleştirir.
</p>

---

### Dosya İşlemleri Nedir?
<p align="left">
Dosya işlemleri, bir bilgisayar sistemindeki dosyalara erişmek ve bu dosyaları okumak, yazmak, oluşturmak, silmek veya değiştirmek için yapılan işlemleri ifade eder. Bu işlemler, genellikle dosyaların veri okuma ve yazma işlemlerini içerir ve dosya sistemine erişim sağlamak için kullanılır. Dosya işlemleri, programların verileri kalıcı olarak depolamak ve gerektiğinde erişmek için dosyaları kullanmasına olanak tanır.
</p>

---

### Karakter İşlemleri Nedir?
<p align="left">
Karakter işlemleri, genellikle bir karakterin belirli bir özelliğe sahip olup olmadığını kontrol etmek için kullanılan işlemlerdir. Örneğin, bir karakterin bir harf olup olmadığını, bir rakam olup olmadığını, bir yazdırılabilir karakter olup olmadığını veya bir ASCII karakteri olup olmadığını belirlemek gibi işlemleri içerir. Bu tür işlemler, genellikle karakter dizilerini veya kullanıcıdan alınan girdileri işlerken karakterlerin özelliklerini kontrol etmek için kullanılır.
</p>

---

### Liste İşlemleri Nedir?
<p align="left">
Liste işlemleri, verilerin düğüm adı verilen birimler halinde organize edilmesi ve işlenmesi için kullanılan işlevlerdir. Bu işlevler, bir veri yapısında yeni bir düğüm oluşturmak, düğüm eklemek, düğüm silmek, düğüm aramak, düğüm sayısını hesaplamak gibi çeşitli işlemleri gerçekleştirir.
</p>

---

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

---

### Calloc Nedir?
<p align="left">
calloc, bellek tahsis etmek için kullanılan bir işlevdir. "Calloc" kelimesi "continuous allocation" kelimelerinin kısaltmasıdır. calloc, bellek tahsis etmek için malloc işlevi gibi kullanılır, ancak farklı olarak ayrılan belleği sıfırlar, yani tüm byte'ları sıfır değeriyle doldurur.
</p>

---

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

---

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

---

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

---

### size_t Nedir? 
<p align="left">
size_t, C ve C++ gibi dillerde kullanılan bir tamsayı türüdür. Bu tür, bellek adresleme ve dizi indeksleme gibi boyutları ifade etmek için genellikle kullanılır. Platforma bağlı olarak değişebilir ve genellikle en büyük adreslenebilir bellek miktarını temsil eder. Örneğin, bir dizinin boyutunu veya bir bellek bloğunun boyutunu temsil etmek için kullanılabilir. size_t, stddef.h başlık dosyasında tanımlanır.
</p>

---

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

---

