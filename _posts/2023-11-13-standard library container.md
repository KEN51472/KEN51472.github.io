---
layout: detail
type : 2
keyword : Standard Library Container
title: Standard Library Container
description: 
---

## 模板的基本语法

函数模板：
```c
template <class T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

```

在上面的例子中，template <class T> 表示这是一个模板函数，T 是一个模板参数，表示函数可以接受任意类型的参数。在函数体中，使用 T 来定义变量、参数和返回值的类型。

类模板：
```c
template <class T>
class Stack {
public:
    void push(T value);
    T pop();
private:
    T data[100];
    int top;
};
```

在上面的例子中，template <class T> 表示这是一个模板类，T 是一个模板参数，表示类可以使用任意类型的数据。在类的成员函数或成员变量中，使用 T 来定义数据类型。

## 模板的使用

调用上述模板
```c
int a = 10, b = 20;
int result = max(a, b); // 调用 max 模板函数

Stack<int> intStack; // 实例化 Stack 模板类，使用 int 类型
intStack.push(10);
int value = intStack.pop();
```
max 函数和 Stack 类都是通过模板定义的，使用不同的数据类型来调用和实例化。

## 模板应用场景

通用数据结构和算法：

```c
template <class T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

int maxInt = max(5, 10); // 使用模板函数计算整数的最大值
double maxDouble = max(3.14, 2.71); // 使用模板函数计算浮点数的最大值
```

容器类和容器算法：

```c
std::vector<int> intVector = {1, 2, 3, 4, 5};
std::sort(intVector.begin(), intVector.end()); // 使用模板函数对整数向量进行排序

std::vector<double> doubleVector = {3.14, 2.71, 1.41};
std::sort(doubleVector.begin(), doubleVector.end()); // 使用模板函数对浮点数向量进行排序
```

泛型编程：

```c
template <class T>
class Pair {
public:
    T first;
    T second;
};

Pair<int> intPair = {10, 20}; // 使用模板类创建整数对
Pair<double> doublePair = {3.14, 2.71}; // 使用模板类创建浮点数对
```

元编程：

```c
template <int N>
struct Factorial {
    static const int value = N * Factorial<N-1>::value;
};

template <>
struct Factorial<0> {
    static const int value = 1;
};

int fact5 = Factorial<5>::value; // 在编译期间计算5的阶乘
```