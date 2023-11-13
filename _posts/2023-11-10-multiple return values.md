---
layout: detail
type : 2
keyword : Multiple Return Values
title: Multiple Return Values
description: 
---

## 函数返回多个值

通过以下几种方法实现多个返回值：

1. 结构体或类：定义一个结构体或类，将需要返回的多个值作为结构体或类的成员，然后在函数中创建一个对象并返回。
```c
struct Result {
    int value1;
    double value2;
};

Result myFunction() {
    Result result;
    result.value1 = 10;
    result.value2 = 3.14;
    return result;
}
```

2. 引用参数：通过函数的参数传递引用，然后在函数内部修改这些参数的值，从而实现多个返回值。
```c
void myFunction(int& value1, double& value2) {
    value1 = 10;
    value2 = 3.14;
}

// 调用方式
int v1;
double v2;
myFunction(v1, v2);
```

3. 元组（C++11及以上版本）：使用标准库中的std::tuple或std::pair可以将多个值打包返回。
```c
#include <tuple>

std::tuple<int, double> myFunction() {
    return std::make_tuple(10, 3.14);
}
```




