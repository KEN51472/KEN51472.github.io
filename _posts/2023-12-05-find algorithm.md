---
layout: detail
type : 2
keyword :     
title: tree
description: 
---

## 二分查找

需要在一个有序数组中查找特定元素时，二分查找是一种非常高效的查找算法。它通过不断缩小查找范围，以每次查找的中间元素为基准，来快速定位目标元素的位置。

```c
#include <iostream>
#include <vector>
using namespace std;

// 二分查找算法
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid; // 找到目标元素，返回索引
        } else if (arr[mid] < target) {
            left = mid + 1; // 目标元素在右半部分
        } else {
            right = mid - 1; // 目标元素在左半部分
        }
    }
    return -1; // 没有找到目标元素
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17};
    int target = 7;
    int result = binarySearch(arr, target);
    if (result != -1) {
        cout << "目标元素在数组中的位置是：" << result << endl;
    } else {
        cout << "数组中没有目标元素" << endl;
    }
    return 0;
}

```

定义一个有序数组arr，然后使用二分查找算法在数组中查找目标元素target。二分查找算法的关键在于不断缩小查找范围，直到找到目标元素或者确定目标元素不存在。

时间复杂度：二分查找的时间复杂度是O(log n)，其中n是数组的大小。因为二分查找是基于有序数组的，因此适用于静态数据集。
空间复杂度：二分查找的空间复杂度是O(1)，因为它只需要几个额外的变量来存储辅助信息。
适用场景：二分查找适用于有序数组的查找，特别是对于静态数据集和需要范围查询的情况。例如，在数据库中，有序索引适用于范围查询和排序操作。

## 哈希查找

哈希查找是利用哈希表来实现的，它通过将元素的关键字作为哈希函数的输入，将元素存储在哈希表的对应位置，然后根据关键字直接在哈希表中查找元素。
```c
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<string, int> hashTable; // 哈希表
    hashTable["apple"] = 10;
    hashTable["banana"] = 20;
    hashTable["orange"] = 30;

    string target = "banana";
    if (hashTable.count(target) > 0) {
        cout << "目标元素" << target << "的值是：" << hashTable[target] << endl;
    } else {
        cout << "哈希表中没有目标元素" << endl;
    }
    return 0;
}
```

使用C++的unordered_map来实现哈希表，然后将一些键值对存储在哈希表中。使用哈希查找来查找目标元素target。哈希查找的关键在于通过哈希函数将关键字映射到哈希表的位置，然后直接在该位置查找元素。

时间复杂度：在理想情况下，哈希查找的时间复杂度是O(1)，即常数时间。但在存在哈希冲突的情况下，时间复杂度可能会上升，但通常仍然是O(1)级别。
空间复杂度：哈希表的空间复杂度取决于哈希表的大小和元素的数量，通常情况下是O(n)。
适用场景：哈希查找适用于需要快速查找、插入和删除操作的场景，尤其是对于静态数据集和需要快速等值查询的情况。例如，数据库中的哈希索引适用于等值查询。