---
theme: seriph
fonts:
  mono: 'Cascadia Code'
layout: center
---

<div class="text-3xl">

- 当我们在谈计算机科学时，其实是在谈什么？
- 当我们在谈编程时，其实是在谈什么？

</div>

---
layout: statement
---

# 解决问题

---
layout: center
---

![](https://cs50.harvard.edu/x/2023/notes/0/cs50Week0Slide38.png)

---
layout: center
---

<div class="text-3xl">

- 数据的流转
- 函数的组合
- 内存的操作

</div>

---
layout: cover
background: https://upload.wikimedia.org/wikipedia/commons/d/db/Swissbit_2GB_PC2-5300U-555.jpg
---

# Memory

---
layout: image
image: https://upload.wikimedia.org/wikipedia/commons/d/db/Swissbit_2GB_PC2-5300U-555.jpg
---



---

## 两数之和

```c
#include <stdio.h>

int add(int a, int b) {
  return a + b;
}

int main(void) {
  printf("%d\n", add(1, 2));
  return 0;
}
```

---

## 两数组之和 🧐

```c
int* array_add(const int a[], size_t a_length, const int b[], size_t b_length) {
  int concatenated[N] = {0};
  size_t length = 0;
  for (size_t i = 0; i < a_length; i++) {
    concatenated[length++] = a[i];
  }
  for (size_t i = 0; i < b_length; i++) {
    concatenated[length++] = b[i];
  }
  return concatenated;
}
```

---

## 问题

1. 变量生存期为函数内部，不可自由控制。
2. 所分配内存大小需在编译期确定。

---
layout: statement
---

# 栈（Stack）

---

## 动态内存分配

- 分配：`malloc`
- 释放：`free`

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
  int* a = malloc(sizeof(int));
  *a = 1;
  printf("%d\n", *a);
  free(a);
  return 0;
}
```

---

## 两数组之和（正确的 😄）

```c
#include <stdlib.h>

int* array_add(const int a[], size_t a_length, const int b[], size_t b_length) {
  int* concatenated = calloc(a_length + b_length, sizeof(int));
  size_t length = 0;
  for (size_t i = 0; i < a_length; i++) {
    concatenated[length++] = a[i];
  }
  for (size_t i = 0; i < b_length; i++) {
    concatenated[length++] = b[i];
  }
  return concatenated;
}
```

---
layout: statement
---

# 堆（Heap）

--- 

## VLA

<https://jorengarenar.github.io/blog/vla-pitfalls>

---

## 易出现的问题

- 内存泄漏
- 二次释放
- 空指针
- 野指针
- 悬垂指针

---

## 解决方法

- 垃圾回收
- RC、ARC：Swift、Objective-C
- RAII、所有权、生命周期、智能指针：Rust、C++
- 多种分配器、`defer`：Zig

---

## 栈 vs 堆

|                  | 栈                         | 堆                         |
| ---------------- | -------------------------- | -------------------------- |
| **管理者**       | 编译器                     | 开发者                     |
| **申请方式**     | 编译器自动分配             | 开发者通过调用函数手动分配 |
| **生命周期**     | 局部变量所在上下文的作用域 | 手动申请后，手动释放前     |
| **可申请空间**   | 小                         | 大                         |
| **效率**         | 高                         | 低                         |
| **地址增长方向** | 由大到小                   | 由小到大                   |

---

## 其他内存区域

- 全局变量区（静态变量区）
- 常量区

---

## 字符串字面量

```c
#include <stdio.h>

const char* hello() {
  const char* s = "Hello, world!";
  return s;
}

int main(void) {
  const char* s = hello();
  puts(s);
  return 0;
}
```

---

## Credits

[C 的动态内存管理与线性数据结构（一）：介绍与分析 | Daniel’s Blog](https://moecm.com/dynamic-memory-and-linear-structures-in-c-intro/)

## 代码下载

<a href="/memory-code.zip" target="_blank">memory-code.zip</a>

