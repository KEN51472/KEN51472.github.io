---
layout: detail
type : 2
keyword : Range-based for loop
title: Range-based for loop
description: 
---

## 基于范围的循环（Range-based for loop）

C++11引入的一种循环语法，用于遍历容器或数组中的元素。它提供了一种更简洁、更安全的方法来遍历序列中的元素。

基本语法：

```c
for (auto element : container) {
    // 使用 element 进行操作
}

```

container是一个容器（比如std::vector、std::array、std::list等）或者一个数组，element是容器中的元素的副本。
在每次迭代中，element会依次取到容器中的每个元素的值，然后你可以在循环体中使用element进行操作。

使用基于范围的循环遍历std::vector：


```c
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    for (auto element : vec) {
        std::cout << element << " ";
    }

    return 0;
}

```

输出1 2 3 4 5，它使用基于范围的循环遍历了std::vector中的所有元素，并将它们输出到标准输出流中。

基于范围的循环可以让代码更加简洁、易读，并且避免了手动处理迭代器的复杂性。它是C++11引入的一个非常有用的特性，可以帮助你更方便地遍历容器中的元素。