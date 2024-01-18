---
layout: detail
type : 2
keyword : function pointer    
title: function pointer
description: 
---

## 函数指针

函数指针在C和C++中是指向函数而不是数据的指针。它们用于将函数作为参数传递给其他函数，从其他函数返回函数，并将函数存储在数据结构（如数组或链表）中

声明函数指针：
指定它指向的函数的返回类型和参数类型，然后是一个星号(*)和指针的名称。eg:声明一个指向接受两个整数并返回一个整数的函数的函数指针

```c
int (*ptr)(int, int);

```
声明了函数指针后，使用取地址运算符（&）和函数名称将其赋值为函数的地址

```c

int add(int a, int b) {
    return a + b;
}

int (*ptr)(int, int) = &add;

```

通过指针使用解引用运算符(*)调用函数

```c
int result = (*ptr)(2, 3);

```

函数指针经常用于回调机制，其中函数作为参数传递给另一个函数，以便在以后的某个时间调用。它们还用于在面向对象编程中实现多态性和动态调度，根据对象类型调用不同的函数


## 应用场景


底层的类需要向高层的类传递信息时，需要回调：

```c
#include <iostream>

// 定义回调接口
class CallbackInterface {
public:
    virtual void OnEventOccur() = 0;
};

// 类A实现回调接口
class ClassA : public CallbackInterface {
public:
    void DoSomethingWithB() {
        // 创建类B的实例
        ClassB b;
        // 将类A自身作为回调传递给类B
        b.RegisterCallback(this);
        // 调用类B的方法
        b.DoSomething();
    }

    // 实现回调接口的方法
    virtual void OnEventOccur() override {
        std::cout << "ClassA has been notified of the event." << std::endl;
    }
};

// 类B
class ClassB {
private:
    CallbackInterface* callback;

public:
    // 注册回调
    void RegisterCallback(CallbackInterface* cb) {
        callback = cb;
    }

    // 类B的方法
    void DoSomething() {
        // 执行一些操作
        std::cout << "ClassB is doing something." << std::endl;

        // 当事件发生时，通知类A
        if (callback != nullptr) {
            callback->OnEventOccur();
        }
    }
};

int main() {
    // 创建类A的实例
    ClassA a;
    // 类A调用类B的方法
    a.DoSomethingWithB();

    return 0;
}

```

定义一个CallbackInterface回调接口，类A实现了这个接口，并在调用类B的方法时将自身作为回调传递给类B。类B在需要通知类A时，调用回调接口的方法来触发类A的相应操作。类B不再依赖于类A，只是依赖于回调接口