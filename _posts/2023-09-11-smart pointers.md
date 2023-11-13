---
layout: detail
type : 2
keyword : 智能指针
title: 智能指针
description: smart pointers
---

## smart pointers

原始指针直接操作内存地址，它不会自动管理所指向的资源的内存，需要手动进行内存的分配和释放。如果忘记释放内存或者释放了正在使用的内存，就会导致内存泄漏或者悬垂指针等问题。

智能指针是一种封装了原始指针的对象，可以自动管理所指向的资源的内存。智能指针使用一些策略来确保在不再需要资源时，自动释放内存。这些智能指针使用了引用计数、独占所有权和弱引用等机制来管理资源的生命周期。

相对于原始指针，智能指针的主要优势在于它们可以提供自动的内存管理，减少了手动分配和释放内存的繁琐工作，同时也减少了内存泄漏和悬垂指针等错误的可能性。

在智能指针中，RAII 的概念得到了很好的体现。智能指针在构造时会自动分配所管理的资源，并在析构时自动释放这些资源。


# Unique Pointers (std::unique_ptr<>)

由于 unique_ptr 维护资源的唯一所有权，因此无法对其进行复制，删除了复制构造函数和复制赋值运算符，只能使用移动语义将指针的所有权从一个指针对象转移/移动到另一个指针对象

```c
std::unique_ptr<Thing> p1 (new Thing); // p1 owns the Thing
std::unique_ptr<Thing> p2(p1); // error - copy construction is not allowed.
std::unique_ptr<Thing> p3; // an empty unique_ptr;
p3 = p1; // error, copy assignment is not allowed.

std::unique_ptr<Thing> up1;
std::unique_ptr<Thing> up2(new Thing);
up1 = std::move(up2); // ownership transfer using move semantics is allowed

```

std::unique_ptr 作为函数参数传递 

```c
void foo(std::unique_ptr<std::string> cp) {
 //...
}

//call foo

auto up = std::make_unique<std::string>("some string");

foo(up); //!ERROR. No copy allowed.

foo(std::move(up)); //OK. Explicit move

foo(std::make_unique<std::string>("some string")); //OK. Implicit move
```

# Shared Pointers (std::shared_ptr<>)

同一个对象可能被多个对象拥有,当最后一个shared_ptr被销毁或通过operator=与reset()分配另一个指 针后，对象将被销毁并释放其内存：

创建更多的指针副本及它们退出作用域时，引用计数会相应地增加和减少。当引用计数达到零时，底层内存被释放

shared_ptr 与 虚拟析构函数：

未使用智能指针时，因为基类Base并没有virtual，所以子类Derived并没有正确被析构，可能会导致内存泄漏：
```c
struct Base
{
    ~Base()
    {
        std::cout << "Base::~Base()\n";
    }
};

struct Derived: public Base
{
    ~Derived()
    {
        std::cout << "Derived::~Derived()\n";
    }
};

int main()
{
    Base* base = new Derived;
    delete base; // prints Base::~Base(), hence Derived class object is partially destructed
    return EXIT_SUCCESS;
}

```

使用智能指针shared_ptr之后，智能指针通过管理单独的控制块来工作，控制块中存储了一个删除器。控制块的删除器是在shared_ptr<Derived>创建时就完成设置的。无论发生什么情况，删除器都会调用Derived的析构函数来删除对象，与虚拟调度无关。所以不需要Base的虚拟析构函数了。

当基类超出 shared_ptr 范围或重置时，会正确的调用派生类析构函数。

```c
struct Base
{
    ~Base()
    {
        std::cout << "Base::~Base()\n";
    }
};


struct Derived: public Base
{
    ~Derived()
    {
        std::cout << "Derived::~Derived()\n";
    }
};

int main()
{
    std::shared_ptr<Base> base(new Derived);
    return EXIT_SUCCESS;
}

```

std::make_shared 相较于直接使用 std::shared_ptr 的方式有几个优点：

效率更高：std::make_shared 在动态分配内存时，会一次性分配存储对象和控制块的内存，从而减少了内存分配的次数和额外的内存开销,也减少了内存碎片化。相比之下，直接使用 std::shared_ptr 需要分别分配对象和控制块的内存，效率较低。

异常安全性更好：std::make_shared 在内存分配失败时会抛出 std::bad_alloc 异常，而直接使用 std::shared_ptr 则需要在分配对象和控制块的过程中捕获异常并进行处理，代码更复杂，容易出错。

可读性更好：std::make_shared 的语法更简洁，易于理解和阅读。它将对象的创建和智能指针的初始化合并在一起，使代码更加清晰。

综上使用 std::make_shared 来创建 std::shared_ptr 对象，以获得更高的效率、更好的异常安全性和更好的可读性。



# Weak pointer std::weak_ptr<>

解决shared_ptr因为循环引用导致的析构未正确调用的问题
使用weak_ptr后，A拥有B但B不拥有A，
```c
#include <memory>
#include <iostream>

struct MyClassB;
struct MyClassA
{
    std::shared_ptr<MyClassB> b;
    ~MyClassA() { std::cout << "MyClassA::~MyClassA()\n"; }
};

struct MyClassB
{
    std::weak_ptr<MyClassA> a;
    ~MyClassB() { std::cout << "MyClassB::~MyClassB()\n"; }
};

void useMyClassAnMyClassB()
{
    auto a = std::make_shared<MyClassA>();
    auto b = std::make_shared<MyClassB>();
    a->b = b;
    b->a = a;
}

int main()
{
    useMyClassAnMyClassB();
    std::cout << "Finished using A and B\n";
}

```

弱引用的一个主要应用场景是在多个对象之间存在相互引用，而且这些对象的生命周期可能不同。如果只使用shared_ptr进行引用，就会形成循环引用，导致对象无法被销毁，从而产生内存泄漏。通过使用weak_ptr，可以避免循环引用，同时可以在需要时通过调用weak_ptr的lock()获取一个有效的shared_ptr对象来访问所管理的对象

wp.expired()查看weak_ptr是否过期


## 相关网站

[unique_ptr](https://pratikparvati.com/html/blogview.html?id=-Mce2yaFyo-5IU1F8Rq_&lan=cpp)    
[shared_ptr](https://pratikparvati.com/html/blogview.html?id=-Md9Uk5aUhGBdDd4ODH4&lan=cpp)
