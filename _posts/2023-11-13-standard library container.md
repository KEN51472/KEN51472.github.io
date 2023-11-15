---
layout: detail
type : 2
keyword : Standard Library Container
title: Standard Library Container
description: 
---

## vector:
vector是一个动态数组，提供了快速的随机访问和在末尾进行插入和删除操作的能力。
优点：在大多数情况下，vector提供了高效的随机访问和尾部插入/删除的性能。
缺点：在中间或头部插入/删除元素时，需要移动后续元素，效率较低。
```c
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    vec.push_back(6); // 在尾部插入元素
    vec.pop_back(); // 删除尾部元素
    std::cout << vec[2] << std::endl; // 随机访问
    return 0;
}
```

## list:
list是一个双向链表，提供了在任意位置进行高效的插入和删除操作的能力。
优点：在中间或头部插入/删除元素时，list提供了高效的性能。
缺点：由于链表结构，无法进行随机访问，需要遍历整个链表来查找元素。

```c
#include <list>
#include <iostream>

int main() {
    std::list<int> myList = {1, 2, 3, 4, 5};
    myList.push_front(0); // 在头部插入元素
    myList.pop_back(); // 删除尾部元素
    // 无法使用 myList[2] 进行随机访问
    return 0;
}

```

## map:
map是一个关联容器，提供了键-值对的存储和高效的查找操作。
优点：在查找操作时，map提供了高效的性能，时间复杂度为O(log n)。
缺点：相比于unordered_map，map的查找操作稍慢，而且无法保证元素的顺序。

map是基于红黑树实现的，它保持元素的顺序，因此可以进行范围遍历。
unordered_map是基于哈希表实现的，它不保持元素的顺序，因此无法进行范围遍历。

```c
#include <map>
#include <iostream>

int main() {
    std::map<std::string, int> myMap = {{"A", 25}, {"B", 30}, {"C", 20}};
    myMap["David"] = 28; // 插入键值对
    std::cout << myMap["Bob"] << std::endl; // 查找操作
    return 0;
}
```

## 适用场景
高效的随机访问和尾部插入/删除操作，可以选择vector；
需要在任意位置进行高效的插入/删除操作，可以选择list；
需要键-值对的存储和高效的查找操作，可以选择map。                                                                            