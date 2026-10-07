<h1 align="center">🖨️ ft_printf</h1>

<p align="center">
  <img src="https://img.shields.io/badge/language-C-blue" alt="Language: C">
  <img src="https://img.shields.io/badge/norminette-passing-brightgreen" alt="Norminette">
  <img src="https://img.shields.io/badge/42-Common%20Core-black" alt="42 Common Core">
</p>

<p align="center">
  A re-implementation of the C standard <code>printf</code> function, built around variadic arguments.
</p>

---

## 📖 Description

**ft_printf** is a 42 Common Core project whose goal is to recode `printf` from `libc`. It is an introduction to **variadic functions** in C (`va_start`, `va_arg`, `va_end`) and to writing extensible, well-structured code.

The result is a static library, `libftprintf.a`, that can be reused in future 42 projects.

This repository contains the **mandatory part only**: flags, field width and precision (bonus) are not handled.

> [!NOTE]
> Unlike the original `printf`, `ft_printf` does not implement buffer management. Each conversion is written directly with `write`.

### Prototype

```c
int	ft_printf(const char *format, ...);
```

`ft_printf` writes the formatted output to the standard output and returns the number of characters printed, or `-1` on error.

## 🧩 Supported conversions

| Conversion | Description                                                  |
|------------|--------------------------------------------------------------|
| `%c`       | Prints a single character                                    |
| `%s`       | Prints a string (`(null)` if the pointer is `NULL`)          |
| `%p`       | Prints a `void *` pointer address in hexadecimal             |
| `%d`       | Prints a signed decimal integer                              |
| `%i`       | Prints a signed integer in base 10                           |
| `%u`       | Prints an unsigned decimal integer                           |
| `%x`       | Prints a number in lowercase hexadecimal                     |
| `%X`       | Prints a number in uppercase hexadecimal                     |
| `%%`       | Prints a percent sign                                        |

## 🛠️ Instructions

### Requirements

- `cc` (or `gcc` / `clang`)
- `make`
- `ar`

### Compilation

```bash
git clone <repository-url> ft_printf
cd ft_printf
make
```

This produces `libftprintf.a` at the root of the repository. Sources are compiled with `-Wall -Wextra -Werror`.

### Makefile rules

| Rule          | Description                                    |
|---------------|------------------------------------------------|
| `make`        | Compiles the library (`libftprintf.a`)         |
| `make clean`  | Removes object files                           |
| `make fclean` | Removes object files and `libftprintf.a`       |
| `make re`     | Runs `fclean` then `make`                      |

### Usage

Include the header in your code:

```c
#include "ft_printf.h"

int	main(void)
{
	int	len;

	len = ft_printf("Hello %s! You are %d years old.\n", "Marvin", 42);
	ft_printf("Hex: %x | HEX: %X | Ptr: %p | %%\n", 255, 255, &len);
	ft_printf("Printed %d characters.\n", len);
	return (0);
}
```

Then compile with the library:

```bash
cc -Wall -Wextra -Werror main.c -L. -lftprintf -o program
```

Expected output:

```
Hello Marvin! You are 42 years old.
Hex: ff | HEX: FF | Ptr: 0x7ffd... | %
Printed 36 characters.
```

## ⚙️ How it works

1. `ft_printf` walks through the `format` string character by character.
2. Regular characters are written as is.
3. When a `%` is found, the next character determines the conversion, and the matching argument is fetched with `va_arg`.
4. A dedicated function handles each conversion and returns how many characters it wrote.
5. The counts are summed and returned at the end.

> [!TIP]
> Arguments smaller than `int` (like `char`) are promoted to `int` when passed through `...`, so `%c` must be read with `va_arg(args, int)`.

## 📚 Resources

- `man 3 printf` and `man 3 stdarg`
- [cppreference — Variadic functions](https://en.cppreference.com/w/c/variadic)
- [cppreference — printf](https://en.cppreference.com/w/c/io/fprintf)
- [GNU Make manual](https://www.gnu.org/software/make/manual/)


### Use of AI

AI was used to help structure and format this README. All library code was written by hand, without AI assistance.
