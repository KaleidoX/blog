# 分析 6 种变态的 hello world

> [代码来源](https://coolshell.cn/articles/914.html)

### hello world 1

```c
#define _________ }
#define ________ putchar
#define _______ main
#define _(a) ________(a);
#define ______ _______() {
#define __ ______ _(0x48) _(0x65) _(0x6C) _(0x6C)
#define ___ _(0x6F) _(0x2C) _(0x20) _(0x77) _(0x6F)
#define ____  _(0x72) _(0x6C) _(0x64) _(0x21)
#define _____ __ ___ ____ _________
#include <stdio.h>
_____
```

`_____`

> `__ ___ ____ _________`

`__`

> `______ _(0x48) _(0x65) _(0x6C) _(0x6C)`
>
> `______`
>
> > `_______() {`
>
> `_______`
>
> > main
>
> `_`
>
> > `________(a)`
>
> `________`
>
> > `putchar`
>
> `main() {putchar(0x48);putchar(0x65);putchar(0x6C);putchar(0x6C);`

`___`

> _(0x6F) _(0x2C) _(0x20) _(0x77) \_(0x6F)
>
> `putchar(0x6F);putchar(0x2C);putchar(0x20);putchar(0x77);putchar(0x6F);`

`____`

> _(0x72) _(0x6C) _(0x64) _(0x21)
>
> `putchar(0x72);putchar(0x6C);putchar(0x64);putchar(0x21);`

`_________`

> `}`

综上，转换为

```c
#include <stdio.h>
main() {
  putchar(0x48); // H
  putchar(0x65); // e
  putchar(0x6C); // l
  putchar(0x6C); // l
  putchar(0x6F); // o
  putchar(0x2C); // ,
  putchar(0x20); // 空格
  putchar(0x77); // w
  putchar(0x6F); // o
  putchar(0x72); // r
  putchar(0x6C); // l
  putchar(0x64); // d
  putchar(0x21); // !
}
```

### hello world 2

```c
#include <stdio.h>
main()
{
  int x = 0, y[14], *z = &y;
  *(z++) = 0x48;
  *(z++) = y[x++] + 0x1D;
  *(z++) = y[x++] + 0x07;
  *(z++) = y[x++] + 0x00;
  *(z++) = y[x++] + 0x03;
  *(z++) = y[x++] - 0x43;
  *(z++) = y[x++] - 0x0C;
  *(z++) = y[x++] + 0x57;
  *(z++) = y[x++] - 0x08;
  *(z++) = y[x++] + 0x03;
  *(z++) = y[x++] - 0x06;
  *(z++) = y[x++] - 0x08;
  *(z++) = y[x++] - 0x43;
  *(z++) = y[x] - 0x21;
  x = *(--z);
  while (y[x] != NULL)
    putchar(y[x++]);
}
```

> 该部分 通过指针 设置 y 数组每个字段的值 通过 while 循环 输出对应的字符

### hello world 3

```c
#include <stdio.h>
#define __(a) goto a;
#define ___(a) putchar(a);
#define _(a, b) ___(a) __(b);
main()
{
_:
  __(t)
a:
  _('r', g)
b:
  _('$', p)
c:
  _('l', f)
d:
  _(' ', s)
e:
  _('a', s)
f:
  _('o', q)
g:
  _('l', h)
h:
  _('d', n)
i:
  _('e', w)
j:
  _('e', x)
k:
  _('\n', z)
l:
  _('H', l)
m:
  _('X', i)
n:
  _('!', k)
o:
  _('z', q)
p:
  _('q', b)
q:
  _(',', d)
r:
  _('i', l)
s:
  _('w', v)
t:
  _('H', j)
u:
  _('a', a)
v:
  _('o', a)
w:
  _(')', k)
x:
  _('l', c)
y:
  _('\t', g)
z:
  ___(0x0)
}
```

> 套用第一种方式解析

```
a: putchar("r");goto g;
b: putchar("$");goto p;
c: putchar("l");goto f;
d: putchar(" ");goto s;
e: putchar("a");goto s;
f: putchar("o");goto q;
g: putchar("l");goto h;
h: putchar("d");goto n;
i: putchar("e");goto w;
j: putchar("e");goto x;
k: putchar("\n");goto z;
l: putchar("H");goto l;
m: putchar("X");goto i;
n: putchar("!");goto k;
o: putchar("z");goto q;
p: putchar("q");goto b;
q: putchar(",");goto d;
r: putchar("i");goto l;
s: putchar("w");goto v;
t: putchar("H");goto j;
u: putchar("a");goto a;
v: putchar("o");goto a;
w: putchar(")");goto k;
x: putchar("l");goto c;
y: putchar("\t");goto g;
z: putchar(0x0);
```

```c
#include <stdio.h>
main() {
  // goto t;
  putchar("H");
  // goto j;
  putchar("e");
  // goto x;
  putchar("l");
  // goto c;
  putchar("l");
  // goto f;
  putchar("o");
  // goto q;
  putchar(",");
  // goto d;
  putchar(" ");
  // goto s;
  putchar("w");
  // goto v;
  putchar("o");
  // goto a;
  putchar("r");
  // goto g;
  putchar("l");
  // goto h;
  putchar("d");
  // goto n;
  putchar("!");
  // goto k;
  putchar("\n");
  // goto z;
  putchar(0x0);
}
```

> 使用 goto 跳转流程

### hello world 4

```c
int n[] = {0x48, 0x65, 0x6C, 0x6C, 0x6F, 0x2C, 0x20, 0x77, 0x6F, 0x72, 0x6C, 0x64, 0x21, 0x0A, 0x00}, *m = n;
main(n) { putchar(*m) != '\0' ? main(m++) : exit(n++); }
```

> 使用指针输出数组输出 使用递归 遍历所有元素

### hello world 5

```c
main() {
  int i, n[] = {
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << (1 >> 1))) + ((1 << 1) << (1 << 1))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << 1)) + ((1 << 1) << (1 << (1 >> 1))) + (1 << (1 >> 1))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) - ((1 << 1) << (1 << (1 >> 1)))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) - ((1 << 1) << (1 << (1 >> 1)))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) - (1 << (1 >> 1))),
    (((1 << 1) << (1 << 1) << (1 << 1)) + ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) - ((1 << 1) << (1 << (1 >> 1)))),
    ((1 << 1) << (1 << 1) << (1 << 1)),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1)) - (1 << (1 >> 1))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) - (1 << (1 >> 1))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) + (1 << 1)),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << (1 >> 1))) - ((1 << 1) << (1 << (1 >> 1)))),
    (((1 << 1) << (1 << 1) << (1 << 1) << (1 << 1)) - ((1 << 1) << (1 << 1) << (1 << 1)) + ((1 << 1) << (1 << (1 >> 1)))),
    (((1 << 1) << (1 << 1) << (1 << 1)) + (1 << (1 >> 1))),
    (((1 << 1) << (1 << 1)) + ((1 << 1) << (1 << (1 >> 1))) + (1 << (1 >> 1)))
  };
  for (i = (1 >> 1); i < (((1 << 1) << (1 << 1)) + ((1 << 1) << (1 << (1 >> 1))) + (1 << 1)); i++)
    printf("%c", n[i]);
}
```

> 使用 `移位操作符` 以及 `加减` 生成 `Hello, world!` 对应的 字符串编码， 在 `for` 循环中逐个输出

### hello world 6

```cpp
#include <stdio.h>
#define _(_) putchar(_);
int main(void) {
  int i = 0;
  _(++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++i)
  _(++++++++++++++++++++++++++++++++++++++++++++++++++++++++++i)
  _(++++++++++++++i)
  _(--++i)
  _(++++++i)
  _(--------------------------------------------------------------------------------------------------------------------------------------i)
  _(------------------------i)
  _(++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++i)
  _(----------------i)
  _(++++++i)
  _(------------i)
  _(----------------i)
  _(--------------------------------------------------------------------------------------------------------------------------------------i)
  _(----------------------------------------------i)
  return i;
}
```

> `_(_)`
>> `putchar(_)`
> 
> 使用 `自增` 以及 `自减` 生成 `Hello, world!` 对应的 字符串编码，逐个输出。